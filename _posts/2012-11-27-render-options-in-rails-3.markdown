---
layout: post
status: publish
published: true
title: Rails 3 のレンダー オプション (翻訳版)
author: yehudakatz
author_login: yehudakatz
author_email: yehudakatz@engineyard.com
wordpress_id: 321
wordpress_url: http://www.engineyard.co.jp/blog/?p=321
date: 2012-11-27 06:45:26.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">
本記事は<a href="http://www.engineyard.com/blog/2010/render-options-in-rails-3/" target="_blank">英語版ブログで2010年1月18日に公開された記事</a>の翻訳版です。この記事の初稿は Engine Yard Newsletter の 10 月号に掲載されました。これに類似した投稿に興味がある方は、<a href="http://www.engineyard.com/newsletter"><em>Engine Yard Newsletter</em></a> をご購読ください。
Rails 専門家兼コア チーム メンバーの Yehuda Katz 氏、および Rails 専門家兼フルタイム投稿者の Carl Lerche 氏は、「<strong>Inside Rails (Rails の全貌)</strong>」で Rails プラットフォームと Rails の開発に関する専門的なアドバイスと洞察を提示しています。
</div>

これまでのバージョンの Rails で新しいレンダリング オプションを追加するには、レンダー メソッドに対して <code>alias_method_chain</code> を実行し、新しいオプションを追加して、レンダリング パイプラインにある他のコードと競合しないことを祈りながら待つ必要がありました。

Rails 3 では、レンダリング オプションが他と同等に扱われ、プラグイン作成者が使用するのと同じ新しいシステムが内部で使用されます。この機能の使い方を説明する前に、まず Rails でこれがどう使用されているかを見てみましょう。
<pre lang="ruby" escaped="true">ActionController.add_renderer :json do |json, options|
 json = ActiveSupport::JSON.encode(json) unless json.respond_to?(:to_str)
 json = "#{options[:callback]}(#{json})" unless options[:callback].blank?
 self.content_type ||= Mime::JSON
 self.response_body = json
end</pre>
ここでは新しい <code>render :json</code> オプションを作成しています。これは Rails 2.3 の <code>render :json</code> とまったく同じ動作をします。<code>render_json method</code> では、MIME タイプと応答の本文を設定するために Rails 自体で使用される、同じ低レベルの (ただしパブリックの) API を使用します。レンダー オプションを使用するとレンダー パイプラインの残り部分がすべてスキップされるので、通常のテンプレート選択やレンダリング、あるいは追加したオプションに害を与えるような他の内部変更をブロックする必要はありません。

次は、新しいレンダー オプション :pdf を追加する方法です。ここでは JRuby と Flying Saucer ライブラリを使用します。これは HTML と CSS を受け入れて PDF ファイルに変換します。新しいオプションの構文は <code>render :pdf =&gt; "template_name", :css =&gt; %w(main.css print.pdf), :layout =&gt; "print"</code> となります。

この使用方法を理解するために、まず JRuby で Flying Saucer を使用するために必要なコードを確認しましょう。まず Flying Saucer jar (私の Muse git リポジトリから入手できます) を取得する必要があります。次に、Flying Saucer で HTML と CSS を PDF に変換するために必要なコードを記述します。
<pre lang="ruby" escaped="true"># Both of these are .jar files
require "/path/to/itext"
require "/path/to/core-renderer"

module PdfUtils
 def self.string_to_pdf(input_string)
  io = StringIO.new
  renderer = org.xhtmlrenderer.pdf.ITextRenderer.new
  renderer.set_document_from_string_input input_string
  renderer.layout
  renderer.create_pdf(io.to_outputstream)
  io.string # the PDF file in a String
 end
end</pre>
ちょっと長いですが、きちんと機能します。PDF を作成できるようになったので、これをレンダー オプションに書き入れます。
<pre lang="ruby" escaped="true">ActionController.add_renderer :pdf do |template, options|
 css_files = Array.wrap(options.delete(:css))
 css = css_files.map {|file| File.read(file) }.join("\n")

 # Reuse the render semantics to get a string from the
 # template and options
 string = render_to_string template, options

 # Drop in the CSS before the  in a style tag.
 # In practice, you would probably cache the file reads
 # and the merging of the CSS and HTML.
 string.gsub!(%r{}, "
<!--
#{css}
-->

")
 send_data PdfUtils.string_to_pdf(string), :type =&gt; Mime::PDF
end</pre>
PDF の MIME タイプを登録する必要もあります。
<pre lang="ruby" escaped="true">Mime::Type.register "application/pdf", :pdf</pre>
これで、コントローラー内で次を行うことができます。
<pre lang="ruby" escaped="true">class PostsController &lt; ActionController::Base
 def show
  @post = Post.find(params[:id])

  respond_to do |format|
   format.html
   format.pdf
   # or
   format.pdf { render :pdf =&gt; "show", :css =&gt; %w(application print) }
  end
 end
end</pre>
このプロセスでオプションをレンダーに渡す方法についての心配はなくなり、出力を構築して返す方法に集中することができます。便利でしょう?
