---
layout: post
status: publish
published: true
title: Railtie を使った Rails3の拡張 (翻訳版)
author: andrearko
author_login: andrearko
author_email: andrearko@engineyard.com
wordpress_id: 626
wordpress_url: http://www.engineyard.co.jp/blog/?p=626
date: 2013-03-07 10:49:05.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">この記事はコミュニティ ゲスト投稿者兼 Engine Yard OB の Andre Arko 氏から<a href="http://www.engineyard.com/blog/2010/extending-rails-3-with-railties/" target="_blank">英語版ブログで2010年10月3日</a>に寄せられたものです。Arko 氏は 5 年前から Ruby and Rails を使ってウェブ アプリケーションを作成されており、Bundler コア チームのメンバーでもあります。同氏は <a href="http://plexapp.com/">Plex</a> に勤務するかたわら、<a href="http://twitter.com/indirect">@indirect</a> としてのツイートや、<a href="http://andre.arko.net/">andre.arko.net</a> でのブログも公開しています。</div>
<h2>Rails 3.0 の gem プラグイン</h2>
ついに Rails 3.0 がリリースされました。このバージョンには Railtie という、Rails を拡張するための素晴らしい新機能が追加されています。Railtie は Rails 3 のコア コンポーネントの基盤であり、これには Carlhuda さんが何か月もかけて丁寧にリファクタリングを行った成果が活かされています。Rails の機能は、<code>alias_method_chain</code> をまったく使用せずに、従来よりずっと簡単に拡張できるようになりました。

ただ、Rails を拡張するシステムは徹底点検したものの、ドキュメントの方はまだ更新されていません。<a href="http://guides.rubyonrails.org/plugins.html">Rails プラグイン ガイド</a>には、古い Rails 2 スタイルによるプラグインの書き方が説明されているだけです。Ilya Grigorik 氏が <a href="http://www.igvita.com/2010/08/04/rails-3-internals-railtie-creating-plugins/">Railtie &amp; Creating Plugins (Railtie とプラグインの作成)</a> のブログ記事を書かれていますが、これは Railtie プラグインで可能な機能のごく一部に触れているだけです。この投稿では、Railtie プラグインの作成、Rails 初期化プロセスへのフック処理、Railtie プラグインの gem としてのパッケージ化、そして Rails 3 アプリケーションで gem プラグインを使用する方法についてそれぞれ説明したいと思います。
<h2>Railtie プラグインの作成</h2>
Railtie を作成するのは簡単です。単に <a href="http://api.rubyonrails.org/classes/Rails/Railtie.html"><code>::Rails::Railtie</code></a> から継承するクラスを作成するだけです。Railtie のすべてのサブクラスを使用して、Rails アプリケーションが初期化されます。ActionController、ActionView、およびその他の Rails コンポーネントも Railtie なので、作成したプラグインは Rails アプリケーションの第一級メンバーとして動作することができます。正式な Rails コンポーネントで使用されるものと同じメソッドとコンテキストにアクセスできます。次に、Rails アプリケーションの起動時に読み込まれる最小の Railtie のサンプルを挙げます。
<pre lang="ruby" escaped="true">require 'rails'
class MyCoolRailtie &lt; Rails::Railtie
  # railtie code goes here
end</pre>
<a href="http://api.rubyonrails.org/classes/Rails/Railtie.html">Railtie ドキュメント</a>には各 Railtie クラス内で利用できるすべてのメソッドが一覧されていますが、Railtie で何が可能かについては詳しく説明されていません。そこで、Railtie のメソッドを使用して Rails のカスタマイズと拡張を行う方法を示すサンプルの Railtie を、いくつかアルファベット順にご紹介します。
<h3>console</h3>
<code>console</code> メソッドを使用すると、Rails コンソールの起動時に実行されるコードを Railtie によって追加できます。
<pre lang="ruby" escaped="true">console do
  Foo.console_mode!
end</pre>
<h3>generators</h3>
Rails は <code>lib/generators/*.rb</code> で定義されたすべてのジェネレーターを自動的に要求します。<a href="http://api.rubyonrails.org/classes/Rails/Generators.html">Rails::Generators</a> を、別のディレクトリに入っている Railtie と併せて配布する場合は、このメソッドを使って要求することができます。
<pre lang="ruby" escaped="true">generators do
  require 'path/to/generator'
end</pre>
<h3>rake_tasks</h3>
アプリケーション用の rake タスクを Railtie と併せて配布する場合、このメソッドを使って読み込みます。
<pre lang="ruby" escaped="true">rake_tasks do
  require 'path/to/railtie.tasks'
end</pre>
<h3>initializer</h3>
<code>initializer</code> メソッドは Railtie にさまざまな機能を提供します。アプリケーション ディレクトリの <code>config/initializers</code> に配置されるファイルなど、Rails のブート プロセス中に実行される initializer を作成します。initializer メソッドは、自分の initializer の前か後に特定の initializer を実行したい場合に、<code>:after</code> か <code>:before</code> の 2 つのオプションを指定できます。
<pre lang="ruby" escaped="true">initializer "my_cool_railtie.boot_foo" do
  Foo.boot(Bar)
end

initializer "my_cool_railtie.boot_bar",
  :before =&gt; "my_cool_railtie.boot_foo" do
    Bar.boot!
end</pre>
<h2>Rails の設定フック</h2>
Railties で提供される最大の拡張フックには <code>config</code> メソッドという何気ない名前が付いています。このメソッドは、ブートしているアプリケーションに属する <a href="http://api.rubyonrails.org/classes/Rails/Railtie/Configuration.html"><code>Railtie::Configuration</code></a> のインスタンスを返します。<code>config</code> オブジェクトは Rails アプリケーションの <code>environment.rb</code> ファイル内で提供されるものと同じなので、これによっていろいろな面白い操作が可能になります。以下に、<code>config</code> を使って Rails アプリケーションの初期化と設定の方法に変更を加える例をコメント付きでいくつか示します。
<h3>after_initialize</h3>
このメソッドは、Rails が完全に初期化され、アプリケーションの initializer がすべて実行された後で実行されるブロックを受け入れます。
<h3>app_middleware</h3>
このメソッドは、Rails アプリケーションへの要求の処理に使用される <a href="http://api.rubyonrails.org/classes/ActionDispatch/MiddlewareStack.html">MiddlewareStack</a> を公開します。<code>use</code> や <code>swap</code> など、MiddlewareStack で定義されている任意のメソッドを使用して、Rails アプリケーションの Rack ミドルウェアを管理できます。たとえば、Railtie に Rack ミドルウェア <code>MyRailtie::Middleware</code> が含まれている場合、これを Rails アプリケーションのミドルウェア スタックに次のように追加することができます。
<pre lang="ruby" escaped="true">config.middlewares.use MyRailtie::Middleware</pre>
<h3>before_configuration</h3>
このメソッドにブロックとして渡されるコードは、<code>application.rb</code> 内にあるアプリケーション設定ブロックが実行される直前に実行されます。これは通常、下記の <code>jquery-rails</code> の例のように、プラグインのユーザーが自分で上書きできる既定のオプションを設定する最適の場所です。
<h3>before_eager_load</h3>
<code>before_eager_load</code> に渡されたブロックは、Rails がアプリケーションのクラスを要求する前に実行されます。eager load は開発モードで実行されることはありません。しかし、Rails を読み込んだ後、アプリケーション コードが読み込まれる前にコードを実行する必要がある場合には、ここに配置します。
<pre lang="ruby" escaped="true">config.before_eager_load do
  SomeClass.set_important_value = "RoboCop"
end</pre>
<h3>before_initialize</h3>
このメソッドは、Rails の初期化プロセスが開始する前に実行されるブロックを受け入れます。これは基本的には initializer を作成してアプリケーションの最初の initializer の前に実行するよう設定するのと同じ効果があります。
<h3>generators</h3>
このオブジェクトには <code>rails generate</code> コマンドを実行すると呼び出されるジェネレーターの設定が格納されます。
<pre lang="ruby" escaped="true">config.generators do |g|
  g.orm             :datamapper, :migration =&gt; true
  g.template_engine :haml
  g.test_framework  :rspec
end</pre>
これを使ってコンソールで色付きのログを無効にすることもできます。
<pre lang="ruby" escaped="true">config.generators.colorize_logging = false</pre>
<h3>to_prepare</h3>
最後に、<code>to_prepare</code> は重要なメソッドで、1 回限りのセットアップを行うことができます。このメソッドに渡されたブロックは、開発モードでは各要求ごとに実行されますが、本番では 1 度だけ実行されます。これは、アプリケーションが要求の処理を始める前に 1 度だけ何かをセットアップする必要がある場合に使用します。
<h2>サンプル コード</h2>
ここまで読んで、こんなものを使う機会が本当にあるのかと疑っている方も多いと思います。そこで、以下に gem にパッケージ化された Railtie プラグインの例をいくつか挙げることにします。
<h3><a href="http://github.com/rspec/rspec-rails">rspec-rails</a></h3>
rspec-rails プラグインは、<a href="http://github.com/rspec/rspec">RSpec</a> gem を Rails と統合する一連の rake タスクおよびジェネレーターと併せて配布されます。
<pre lang="ruby" escaped="true">module RSpec
  module Rails
    class Railtie &lt; ::Rails::Railtie
      config.generators.integration_tool :rspec
      config.generators.test_framework   :rspec

      rake_tasks do
        load "rspec/rails/tasks/rspec.rake"
      end
    end
  end
end</pre>
この Railtie は 3 つの処理を行います。まず、<code>integration_tool</code> メソッドを使って、統合テストに使用されるジェネレーターを設定します。次に、モデル、コントローラー、およびビュー テストの生成に使用されるジェネレーターを設定します (<code>test_framework</code> メソッドを使用) 。最後に、RSpec rake タスクを読み込んで、test-unit テストの代わりに Spec テストを実行します。
<h3><a href="http://github.com/indirect/jquery-rails">jquery-rails</a></h3>
jquery-rails プラグインはジェネレーターとともに配布されますが、このジェネレーターは jQuery (Rails ヘルパーを jQuery で有効にする jquery-ujs スクリプト) のダウンロードとインストールを行い、オプションで jQueryUI をインストールします。
<pre lang="ruby" escaped="true">module Jquery
  module Rails
    class Railtie &lt; ::Rails::Railtie
      config.before_configuration do
        if ::Rails.root.join('public/javascripts/jquery-ui.min.js').exist?
          config.action_view.javascript_expansions[:defaults] =
            %w(jquery.min jquery-ui.min rails)
        else
          config.action_view.javascript_expansions[:defaults] =
            %w(jquery.min rails)
        end
      end
    end
  end
end</pre>
この Railtie が行う設定は 1 つだけですが、jQueryUI ライブラリをチェックして設定する値を決定します。<code>config.before_configuration</code> フックの使用により、<code>application.rb</code> 設定ブロックが実行される直前に実行されます。したがって、jQueryUI のチェックに必要な Rails.root にアクセスでき、またプラグインの提示する新たな既定値以外の値を使用したいユーザーは、各自の <code>application.rb</code> で <code>javascript_expansion[:defaults]</code> を上書きすることが可能です。
<h3><a href="http://github.com/indirect/haml-rails">haml-rails</a></h3>
haml-rails gem は、ERB で書かれている既定の生成済みビューの代わりに、Haml で書かれたビュー用のジェネレーターを提供します。
<pre lang="ruby" escaped="true">module Haml
  module Rails
    class Railtie &lt; ::Rails::Railtie
      config.generators.template_engine :haml

      config.before_initialize do
        Haml.init_rails(binding)
        Haml::Template.options[:format] = :html5
      end
    end
  end
end</pre>
この Railtie は、<code>rails generate</code> の実行時に Rails によって呼び出されるテンプレート エンジンを変更してから、Haml を Rails 用に初期化して、Haml の出力形式を HTML5 に設定します。
<h2>gem プラグインのパッケージ化</h2>
Railtie プラグインを Rails 用の gem プラグインにするのは簡単です。そのため、配布や管理、アップグレードも容易に行えます。まず必要なのは gem です。gem がまだない場合は、<a href="http://gembundler.com">Bundler</a> を使って新しい gem を簡単に作成できます。<code>bundle gem my_new_gem</code> を実行するだけで、Bundler がスケルトン gem と、ベスト プラクティスに沿った gemspec を生成してくれます。gem ができたら、<code>lib/my_new_gem.rb</code> の読み込み時に Railtie サブクラスが定義されていることを確認してください。Railtie を個別のファイルに定義してそのファイルを要求するか、あるいは直接定義することもできます。最後に、Rails gem への依存関係 (~&gt;3.0) を gemspec に追加します。

作成した gem が標準の Ruby ライブラリでもあり、Rails gem に依存したくない場合は、Railtie を別個のファイルに配置して、メイン ライブラリ ファイル内でそのファイルを条件付きで要求することができます。
<pre lang="ruby" escaped="true"># lib/my_new_gem/my_cool_railtie.rb
module MyNewGem
  class MyCoolRailtie &lt; ::Rails::Railtie
    # Railtie code here
  end
end</pre>
<pre lang="ruby" escaped="true"># lib/my_new_gem.rb
require 'my_new_gem/my_cool_railtie.rb' if defined?(Rails)</pre>
これにより、gem が Rails アプリケーションのコンテキスト外で読み込まれる場合に、Railtie なしでの読み込み可能になります。

これで gem に Railtie を追加できました。次は、これを構築して <a href="http://gemcutter.org">Gemcutter</a> にリリースします。gem が Gemcutter にリリースされたら、Rails 3 アプリケーションで使用するのはごく簡単です。gem を <code>Gemfile</code> に追加するだけです。<code>bundle install</code> を実行すると、Bundler がその gem をダウンロードしてインストールし、Rails がこれを読み込んで、あとは <code>Rails::Railtie</code> クラスがすべて処理してくれます。
