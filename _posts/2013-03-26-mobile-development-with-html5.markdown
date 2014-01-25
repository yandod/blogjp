---
layout: post
status: publish
published: true
title: HTML5 を使ったモバイル 開発 (翻訳版)
author: christosswill
author_login: christosswill
author_email: christosswill@engineyard.com
excerpt: "<div class=\"note\">\r\n本記事は<a href=\"http://www.engineyard.com/blog/2011/mobile-development-with-html5/\"
  target=\"_blank\">英語版ブログに2011年8月25日に公開された記事</a>の翻訳版です。\r\n</div>\r\n\r\n<h3>HTML5:
  標準、流行語、そして伝説</h3>\r\n技術畑になんらかの関係があるブログを読んでいる方なら、ほぼ毎週のように HTML5 についての記事が目に入ると思います。万能とはいきませんが、この新しいウェブ標準には、HTML、CSS、そして
  JavaScript だけを使ってパワフルなアプリケーションを作成できる機能が備わっています (Rails のバックエンドにより、これにさらに強力な機能が加えられます)。この投稿では
  HTML5 の主な概念と機能にいくつか触れ、より高度なトピックを扱うための準備をしていきます。\r\n<h3>ブラウザーとの互換性</h3>\r\nおそらくウェブベースのアプリケーションを開発するにあたっての一番の課題は、今日使用されている多岐にわたるブラウザーとの互換性を確保することでしょう。幸い、モバイル
  アプリケーションにおいてはこの問題が軽減されます。一般に携帯電話はコンピューターよりも頻繁に買い替えられ、またスマートフォンは比較的新しい製品分野であることから、市場に浸透している旧式のスマートフォンはそれほど多くありません。しかし、だからと言ってすべてが自由になるわけではありません。シミュレーションだけでなく、サポートするすべてのデバイスで貴社のサイトをテストする必要があります。\r\n<h3>ビューポート</h3>\r\nモバイル
  ブラウザー用ではないウェブサイトにアクセスすると、ページがまずズームアウトした状態で表示されます。これは、モバイル ブラウザーでウェブサイトを表示できるようにするための意図的な処理です。ビューポートの既定幅は
  800 ～ 980 ピクセル (ブラウザーによって異なる) に設定されます。これにより、ユーザーがウェブサイト全体を表示してから、必要に応じてズームインできるようになります。しかし、モバイル専用のウェブサイトを手がけている場合は、初期のビューポートをモバイル
  デバイス向けに設定するとよいでしょう。これには viewport という meta タグを使用します。\r\n<pre lang=\"html\" escaped=\"true\">&lt;meta
  name=\"viewport\" content = \"width=device-width”&gt;</pre>\r\nこの場合、ビューポートがデバイスの幅に設定されるので、コンテンツがまずズームアウトした状態で表示されることはありません。ユーザーが間違ってズームアウトしてしまい
  UI の外観が損なわれるのを避けるには、ズーム機能全体を無効にすると便利です。これには、user-scalable の値を no に設定します。\r\n<pre
  lang=\"html\" escaped=\"true\">&lt;meta name=\"viewport\" content = \"width=device-width
  ,  user-scalable=no\"&gt;</pre>\r\n現在一部のサイトではビューポートの幅が 320 にハードコードされています。これは、iPhone
  の幅が 320 だからです。しかし一般的には、320 ではなく device-width を使用する方が適しています。\r\n\r\n<a href=\"http://www.engineyard.com/blog/wp-content/uploads/A4jFz.png\"><img
  class=\"aligncenter size-full wp-image-10318\" title=\"A4jFz\" src=\"http://www.engineyard.com/blog/wp-content/uploads/A4jFz.png\"
  alt=\"\" width=\"610\" height=\"436\" /></a>\r\n\r\nサイトをモバイル用の正しいサイズに設定できるのは便利ですが、キャッシュ
  マニフェストによるキャッシュとローカル ストレージという HTML5 の 2 つの機能を使うと、完全な機能をもつオフライン サイトが可能になります。\r\n<h3>HTML5
  のキャッシュ機能</h3>\r\nHTML5 のキャッシュ機能では、ユーザーがウェブに接続していなくても、以前にアクセスしたウェブサイトを表示することができます。これは、アプリケーションの使用場所からネットに接続できないユーザーにとって大変便利なだけでなく、接続の一時的遮断の問題を緩和することもできます。\r\n\r\nHTML5
  のキャッシュをセットアップするには、キャッシュに保存したいすべてのページの html タグにマニフェスト ファイルを追加します。"
wordpress_id: 646
wordpress_url: http://www.engineyard.co.jp/blog/?p=646
date: 2013-03-26 09:00:29.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">
本記事は<a href="http://www.engineyard.com/blog/2011/mobile-development-with-html5/" target="_blank">英語版ブログに2011年8月25日に公開された記事</a>の翻訳版です。
</div>

<h3>HTML5: 標準、流行語、そして伝説</h3>
技術畑になんらかの関係があるブログを読んでいる方なら、ほぼ毎週のように HTML5 についての記事が目に入ると思います。万能とはいきませんが、この新しいウェブ標準には、HTML、CSS、そして JavaScript だけを使ってパワフルなアプリケーションを作成できる機能が備わっています (Rails のバックエンドにより、これにさらに強力な機能が加えられます)。この投稿では HTML5 の主な概念と機能にいくつか触れ、より高度なトピックを扱うための準備をしていきます。
<h3>ブラウザーとの互換性</h3>
おそらくウェブベースのアプリケーションを開発するにあたっての一番の課題は、今日使用されている多岐にわたるブラウザーとの互換性を確保することでしょう。幸い、モバイル アプリケーションにおいてはこの問題が軽減されます。一般に携帯電話はコンピューターよりも頻繁に買い替えられ、またスマートフォンは比較的新しい製品分野であることから、市場に浸透している旧式のスマートフォンはそれほど多くありません。しかし、だからと言ってすべてが自由になるわけではありません。シミュレーションだけでなく、サポートするすべてのデバイスで貴社のサイトをテストする必要があります。
<h3>ビューポート</h3>
モバイル ブラウザー用ではないウェブサイトにアクセスすると、ページがまずズームアウトした状態で表示されます。これは、モバイル ブラウザーでウェブサイトを表示できるようにするための意図的な処理です。ビューポートの既定幅は 800 ～ 980 ピクセル (ブラウザーによって異なる) に設定されます。これにより、ユーザーがウェブサイト全体を表示してから、必要に応じてズームインできるようになります。しかし、モバイル専用のウェブサイトを手がけている場合は、初期のビューポートをモバイル デバイス向けに設定するとよいでしょう。これには viewport という meta タグを使用します。
<pre lang="html" escaped="true">&lt;meta name="viewport" content = "width=device-width”&gt;</pre>
この場合、ビューポートがデバイスの幅に設定されるので、コンテンツがまずズームアウトした状態で表示されることはありません。ユーザーが間違ってズームアウトしてしまい UI の外観が損なわれるのを避けるには、ズーム機能全体を無効にすると便利です。これには、user-scalable の値を no に設定します。
<pre lang="html" escaped="true">&lt;meta name="viewport" content = "width=device-width ,  user-scalable=no"&gt;</pre>
現在一部のサイトではビューポートの幅が 320 にハードコードされています。これは、iPhone の幅が 320 だからです。しかし一般的には、320 ではなく device-width を使用する方が適しています。

<a href="http://www.engineyard.com/blog/wp-content/uploads/A4jFz.png"><img class="aligncenter size-full wp-image-10318" title="A4jFz" src="http://www.engineyard.com/blog/wp-content/uploads/A4jFz.png" alt="" width="610" height="436" /></a>

サイトをモバイル用の正しいサイズに設定できるのは便利ですが、キャッシュ マニフェストによるキャッシュとローカル ストレージという HTML5 の 2 つの機能を使うと、完全な機能をもつオフライン サイトが可能になります。
<h3>HTML5 のキャッシュ機能</h3>
HTML5 のキャッシュ機能では、ユーザーがウェブに接続していなくても、以前にアクセスしたウェブサイトを表示することができます。これは、アプリケーションの使用場所からネットに接続できないユーザーにとって大変便利なだけでなく、接続の一時的遮断の問題を緩和することもできます。

HTML5 のキャッシュをセットアップするには、キャッシュに保存したいすべてのページの html タグにマニフェスト ファイルを追加します。<a id="more"></a><a id="more-646"></a>
<pre lang="html" escaped="true">&lt;html manifest="/cache.manifest"&gt;</pre>
このファイルは "CACHE MANIFEST" で始まり、その後にアプリケーションがキャッシュに保存するファイルが列挙されます。
<pre lang="text" escaped="true">CACHE MANIFEST
/mystyle.css
/scripts.js
/logo.jpg</pre>
これで、指定されたファイルがオフラインで利用できるようになります。ただ、キャッシュ マニフェストには隠れた罠がたくさんあります。以下で主なものを見ていきますが、詳細は「<a href="http://diveintohtml5.org/offline.html">Dive into HTML5</a>」を一読されるようお勧めします。

まず最初の罠は、既定ではサイトが最近ダウンロードされたファイルではなくキャッシュされたファイルを優先させるため、ブラウザーが前回ページにアクセスした後でキャッシュが変更されていても、ページがリフレッシュされる (または JavaScript から更新を求められる) まではブラウザーに古いページが表示され続けるという点です。それだけでなく、ほとんどのウェブ サーバーが、その提供ファイルをキャッシュするようブラウザーに指示するため、状況はさらに複雑になります。サイトを開発している場合、常に最新のコピーがダウンロードされるように、ウェブ サーバーがキャッシュ マニフェストをキャッシュしないよう必ず指定してください。

次の大きな罠は、ブラウザーがダウンロード処理を管理する方法に関連しています。ブラウザーはマニフェストが変更されたことを検知すると、すべてのファイルをダウンロードし直します。このプロセスではリソースが大量に消費されるだけでなく、正しくダウンロードできないファイルが 1 つでもあると、ブラウザーは更新を破棄して以前のキャッシュを読み込んでしまいます。この場合、既定ではブラウザーにエラーが一切表示されません。ただし JavaScript を使用して、マニフェストによりスローされたエラーを検知することができます。
<pre lang="javascript" escaped="true">$(function() {
  $(window.applicationCache).bind("error", function() {
    alert("Cache: update failed");
  });
});</pre>
さて、サイトがキャッシュに保存され、すべてが機能するようになりました。しかしサイト公開の準備はまだ完了していません。このキャッシュ手法は静的コンテンツには正しく機能しますが、動的に作成され頻繁に変わるコンテンツがアプリケーションにある場合 (つまり大部分のウェブ アプリケーションの場合) にはあまり上手く行きません。これは、キャッシュが変更されない限り、新しいコンテンツのあるページではなく、古い html ページが表示されてしまうからです。シンプルな解決策は、新しいコンテンツが追加されるたびにキャッシュ マニフェスト ファイルを変更することです。しかし、この方法ではコンテンツが変更されるたびにすべてのファイルをダウンロードし直すようブラウザーに強制することになり、コンテンツが頻繁に更新される場合はリソースの大量消費につながるので、一般的には好ましくありません。解決策は、jQuery テンプレートを使ってページを動的に構築することです。
<h3>jQuery テンプレート</h3>
ベストプラクティスは JavaScript テンプレートを介してコンテンツを入力する方法です。この方法ではコンテンツが HTML ページの一部ではないので、キャッシュ マニフェストによってキャッシュされません。これを行うには、jQuery および jQuery <a href="https://github.com/jquery/jquery-tmpl">テンプレート プラグイン</a>をダウンロードして、アプリケーションに追加する必要があります。

これらのテンプレートの使用には次の 3 つの手順があります。
<ol>
	<li>テンプレートを定義する。</li>
	<li>コレクションを定義する。</li>
	<li>jQuery に対し、テンプレートを使ってページにコンテンツを入力するよう指示する。</li>
</ol>
<h4>以下はシンプルなブログ アプリケーションの例です。</h4>
1.テンプレートを定義します。
<pre lang="html" escaped="true">&lt;script id="post_template" type="text/html”&gt;
&lt;div&gt;

&lt;h2&gt;${Name}&lt;/h2&gt;

&lt;p&gt;${Body}&lt;/p&gt;

&lt;/div&gt;

&lt;/script&gt;</pre>
2.(JSON のポストの) コレクションを定義します。
<pre lang="javascript" escaped="true">&lt;script&gt;
var posts = [
{ Name: "First!", Body: "This is pretty cool" },
{ Name: "Another post", Body: "This is pretty cool" },
{ Name: "Yet another blog post", Body: "This is pretty cool" }];
&lt;/script&gt;</pre>
3.jQuery に対し、テンプレートを使ってページにコンテンツを入力するよう指示します。
<pre lang="javascript" escaped="true">&lt;script&gt;
$( "#post_template" ).tmpl( posts ).appendTo( "#blog_posts" );
&lt;/script&gt;

…

&lt;body&gt;

&lt;div id="blog_posts"&gt;&lt;/div&gt;

&lt;/body&gt;</pre>
このコンテンツは JavaScript 経由で読み込まれますが、動的ではありません。ページ上で定義されているだけです。動的なコンテンツの場合、サーバーの提供する JSON を使用することになります。ここではブログ アプリケーションによって、この URL にあるブログの JSON 表現が提供されると仮定します。
<pre lang="html" escaped="true">/posts.json</pre>
jQueryto に対して、JSON を要求し、これを使ってページに入力するよう指示します。
<pre lang="javascript" escaped="true">&lt;script type="text/javascript"&gt;
$.getJSON('/posts.json', function(data) {
$( "#post_template" ).tmpl( data ).appendTo( "#blog_posts" );
});
&lt;/script&gt;</pre>
また、Name の代わりに post.name を、Post の代わりに post.body を使用するようテンプレートを変更して、テンプレートが JSON 要素を処理できるようにする必要もあります。
<pre lang="javascript" escaped="true">&lt;script id="post_template" type="text/html"&gt;
&lt;div&gt;
  &lt;h2&gt;${post.name}&lt;/h2&gt;
  &lt;p&gt;${post.body}&lt;/p&gt;
&lt;/div&gt;
&lt;/script&gt;</pre>
これで、ブログがキャッシュ マニフェストにキャッシュされていないコンテンツを取得して、jQuery テンプレートを使ってページに入力できるようになりました。ただし、これが機能するのは、モバイル ブラウザーがサーバーに接続できる場合だけです。二歩進んで三歩下がるようですが、正しく機能するモバイル HTML5 アプリケーションがもうすぐ出来上がりますので、安心してください。あとは HTML5 の最後のコンポーネントであるローカル ストレージを追加するだけです。
<h3>ローカル ストレージ</h3>
Webvanta の Christopher Haupt 氏が最近ローカル ストレージに関するゲスト ブログ投稿をされました。詳細とその一般用法は、「<a href="http://www.engineyard.com/blog/2011/enhancing-client-side-storage-with-html5/">Enhancing Client-side Storage with HTML5 (HTML5 におけるクライアントサイド ストレージの強化)</a>」の記事を参照してください。

高いレベルでは、ローカル ストレージはブラウザーにより実装されるクライアントサイドのキーと値のストアです。テキストの文字列をローカルで格納し、これを後で呼び出します。ここではこれを使用して JSON を格納し、サーバーに接続していなくてもブログに投稿内容を表示できるようにします。

これは手作業で書くこともできますが、このプロセスを管理してくれる素晴らしいプラグインがあります。jQuery Offline プラグインは、サーバーにアクセスできない場合はローカル ストレージのコンテンツを使用し、新しいコンテンツを受信した時点でローカル ストレージに格納します。

このプラグインは <a href="https://github.com/wycats/jquery-offline">jQuery-Offline</a> からダウンロードしてください。

このプラグインを使用するには、getJSON の呼び出しを retrieveJSON に変更します。また、getJSON と retrieveJSON には 1 つ重要な違いがあるので、スクリプトを若干変更する必要があります。後者はキャッシュからのプルとサーバーからの新コンテンツ取得のために、2 度実行されます。このため、新しい投稿をページの最後に単に追加すると、投稿が 2 度表示されます。
<pre lang="javascript" escaped="true">&lt;script type="text/javascript"&gt;
$.retrieveJSON('/posts.json', function(data) {
$( "#blog_posts" ).html($( "#post_template" ).tmpl( data ));

});
&lt;/script&gt;</pre>
これでブログ アプリケーションをオフラインで表示して、モバイル ブラウザーに適したサイズで閲覧できるようになりました。このサンプルは、こちらの <a href="https://github.com/engineyard/offline-blog">offline-blog (オフライン ブログ)</a> からダウンロードできます。

今回はモバイル開発をより容易に行えるようにする技術をいくつか簡単にご紹介しました。今後は人気の MVC フレームワーク Backbone.js など、より高度なトピックについて書いていきたいと思います。
