---
layout: post
status: publish
published: true
title: Sass、Compass、Rails 3.1 のアセット パイプライン (翻訳版)
author: wynnnetherland
author_login: wynnnetherland
author_email: wynnnetherland@engineyard.com
excerpt: "<div class=\"note\">本記事は<a href=\"http://www.engineyard.com/blog/2011/sass-compass-and-the-rails-3-1-asset-pipeline/\"
  target=\"_blank\">英語版ブログで2011年11月3日に公開された記事</a>の翻訳版です。\r\nメモ:今回はダラス市所在の Pure Charity
  社 CTO である Wynn Netherland 氏にゲスト投稿をお願いしました。氏は CSS に関する『<a href=\"http://www.manning.com/netherland/\">Sass
  and Compass in Action (Sass と Compass の活用法)</a>』の共著者であるほか、CSS ギークとしてだけでなく、ウェブ デザイナー兼フロントエンド開発者としても活躍されています。詳しくは
  <a href=\"https://github.com/pengwynn\">GitHub</a> や <a href=\"http://twitter.com/#!/pengwynn\">Twitter</a>
  を参照してください。</div>\r\n<h2 id=\"tldr\">TL;DR</h2>\r\nCompass と Rails 3.1 のアセット パイプラインをうまく連携させてスタイルシート
  アセットの作成、保守、提供を行う方法を改善できますが、スタイルシートの開発中にスピードアップを図るにはセットアップを調整する必要があります。\r\n\r\n動的ウェブ
  ページが誕生して以来、ウェブ開発は二分された状態が続いています。開発者はサーバー側のコードとテンプレートを一か所で管理し、その他すべての静的イメージ、スタイルシート、およびクライアントサイド
  スクリプトを別の場所で管理する傾向にあります。このモデルは、デザイナーが静的ページをウェブ開発者に渡し、開発者がこれをサーバーサイド テンプレートに分解するという、作業者に重点を置いた分割チームのワークフローによってさらに強化されます。スタイルシート、イメージ、そしてスクリプトのことを<em>アセット
  (資産)</em> と呼ぶのも、これがアプリケーション コードで処理する対象ではなく、/public フォルダーに預け入れるものだという観念を象徴しています。<a
  href=\"http://guides.rubyonrails.org/asset_pipeline.html\">Rails 3.1 のアセット パイプライン</a>はこの壁を取り払い、静的アセットがウェブ
  アプリケーションにおけるいわば一級市民として扱われるようにします。イメージ、CoffeeScript、その他多くのコンテンツ タイプを扱えますが、ここではアセット
  パイプラインがスタイルシートの作成者にとってどのような意味を持つかを見ていきたいと思います。\r\n<h2 id=\"whatdoesthepipelinedoforme\">パイプラインで何ができるか</h2>\r\nアセット
  パイプラインは CSS の提供においていくつか大事な役割を果たします。\r\n\r\n<strong>連結機能</strong>。複数のソース ファイルを繋いでスタイルシートを作成し、CSS
  アセットを求める HTTP 要求の数を減らします。Rails 3.1 では既定の application.css がマニフェストで、パイプラインに対してどのソース
  ファイルを連結させてブラウザーに提供するかを指示します。\r\n<pre escaped=\"true\">/*\r\n * This is a manifest
  file that'll automatically include all the stylesheets\r\n * available in this directory
  and any sub-directories. You're free to add\r\n * application-wide styles to this
  file and they'll appear at the top of the\r\n * compiled file, but it's generally
  better to create a new file per style scope.\r\n *= require_self\r\n *= require_tree
  .\r\n */</pre>\r\n既定では、<em>すべて</em>のスタイルシートが含められます。パイプラインの基盤をなす gem である <a href=\"https://github.com/sstephenson/sprockets\">Sprockets</a>
  では、さらに細かい制御が可能です。\r\n<pre escaped=\"true\">/*\r\n *= require vars\r\n *= require
  typography\r\n *= require layout\r\n */</pre>\r\nこれで部分表示 (view partial) と同じく、複数のソース
  ファイルにまたがる大きなスタイルシートを分割して管理できるようになります。"
wordpress_id: 364
wordpress_url: http://www.engineyard.co.jp/blog/?p=364
date: 2013-01-30 09:26:38.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">本記事は<a href="http://www.engineyard.com/blog/2011/sass-compass-and-the-rails-3-1-asset-pipeline/" target="_blank">英語版ブログで2011年11月3日に公開された記事</a>の翻訳版です。
メモ:今回はダラス市所在の Pure Charity 社 CTO である Wynn Netherland 氏にゲスト投稿をお願いしました。氏は CSS に関する『<a href="http://www.manning.com/netherland/">Sass and Compass in Action (Sass と Compass の活用法)</a>』の共著者であるほか、CSS ギークとしてだけでなく、ウェブ デザイナー兼フロントエンド開発者としても活躍されています。詳しくは <a href="https://github.com/pengwynn">GitHub</a> や <a href="http://twitter.com/#!/pengwynn">Twitter</a> を参照してください。</div>
<h2 id="tldr">TL;DR</h2>
Compass と Rails 3.1 のアセット パイプラインをうまく連携させてスタイルシート アセットの作成、保守、提供を行う方法を改善できますが、スタイルシートの開発中にスピードアップを図るにはセットアップを調整する必要があります。

動的ウェブ ページが誕生して以来、ウェブ開発は二分された状態が続いています。開発者はサーバー側のコードとテンプレートを一か所で管理し、その他すべての静的イメージ、スタイルシート、およびクライアントサイド スクリプトを別の場所で管理する傾向にあります。このモデルは、デザイナーが静的ページをウェブ開発者に渡し、開発者がこれをサーバーサイド テンプレートに分解するという、作業者に重点を置いた分割チームのワークフローによってさらに強化されます。スタイルシート、イメージ、そしてスクリプトのことを<em>アセット (資産)</em> と呼ぶのも、これがアプリケーション コードで処理する対象ではなく、/public フォルダーに預け入れるものだという観念を象徴しています。<a href="http://guides.rubyonrails.org/asset_pipeline.html">Rails 3.1 のアセット パイプライン</a>はこの壁を取り払い、静的アセットがウェブ アプリケーションにおけるいわば一級市民として扱われるようにします。イメージ、CoffeeScript、その他多くのコンテンツ タイプを扱えますが、ここではアセット パイプラインがスタイルシートの作成者にとってどのような意味を持つかを見ていきたいと思います。
<h2 id="whatdoesthepipelinedoforme">パイプラインで何ができるか</h2>
アセット パイプラインは CSS の提供においていくつか大事な役割を果たします。

<strong>連結機能</strong>。複数のソース ファイルを繋いでスタイルシートを作成し、CSS アセットを求める HTTP 要求の数を減らします。Rails 3.1 では既定の application.css がマニフェストで、パイプラインに対してどのソース ファイルを連結させてブラウザーに提供するかを指示します。
<pre escaped="true">/*
 * This is a manifest file that'll automatically include all the stylesheets
 * available in this directory and any sub-directories. You're free to add
 * application-wide styles to this file and they'll appear at the top of the
 * compiled file, but it's generally better to create a new file per style scope.
 *= require_self
 *= require_tree .
 */</pre>
既定では、<em>すべて</em>のスタイルシートが含められます。パイプラインの基盤をなす gem である <a href="https://github.com/sstephenson/sprockets">Sprockets</a> では、さらに細かい制御が可能です。
<pre escaped="true">/*
 *= require vars
 *= require typography
 *= require layout
 */</pre>
これで部分表示 (view partial) と同じく、複数のソース ファイルにまたがる大きなスタイルシートを分割して管理できるようになります。<a id="more"></a><a id="more-364"></a>

<strong>縮小機能</strong>。スタイルシートをブラウザーに提供する前に、スペースとコメントを削除してファイル サイズを縮小します。

<strong>フィンガープリント機能</strong>。Rails 3.1 では、キャッシュつぶしを行うフィンガープリント機能がアセットのファイル名に直接組み込まれています。したがって、マルチサーバー環境や一部の透過型プロキシ サーバーに適さないクエリ文字列パラメーターには依存しません。

<strong>事前処理</strong>。アセット パイプラインの一番の特長はその事前処理機能にあると言えるでしょう。スタイルシートを Sass、Less、あるいは ERB でも作成できるので、静的スタイルシートの作成に動的メソッドが導入されます。
<h2 id="compassinthepipeline">パイプラインの Compass</h2>
上記の利点の多くは、Sass のスタイルシート フレームワークである <a href="http://compass-style.org">Compass</a> でこれまで提供されていました。ですから、アセット パイプラインの登場によって Compass は使用廃止となるのかという質問が Compass のメーリング リストに寄せられたのもうなずけます。

Compass とアセット パイプラインでは確かに一部の機能が重複しますが、Compass は他にもできることがたくさんあります。連結、縮小、Sass による事前処理だけでなく、Compass は一般的なスタイルシートのタスク向けに、以下のようなパワフルなモジュールを備えています。
<ul>
	<li><strong>CSS3</strong>。<a href="http://compass-style.org/reference/compass/css3/">Compass CSS3 モジュール</a>は CSS3 機能用の Sass mixin を提供し、単一の構文を使って複数のブラウザーのベンダー名前空間をターゲットにできるようにします。</li>
	<li><strong>CSS スプライト</strong>。HTTP 要求の数を減らすとウェブ アプリケーションのパフォーマンスを大幅に改善できます。<a href="http://compass-style.org/reference/compass/helpers/sprites/">スプライト ヘルパー</a>は個々のアセットが入ったフォルダーから <a href="http://css-tricks.com/158-css-sprites/">CSS スプライト</a>を作成してスプライト レイアウトの配置をすべて処理し、アイコンを名前で参照できるようにします。</li>
	<li><strong>グリッド フレームワーク</strong>。Compass では <a href="http://compass-style.org/reference/blueprint/">Blueprint</a>、<a href="https://github.com/nextmat/compass-960-plugin">960.gs</a>、<a href="https://github.com/ericam/compass-susy-plugin">Susy</a>、<a href="http://grid-coordinates.com/">Grid Coordinates</a> その他がサポートされます。</li>
	<li><strong>ページの仕上がり</strong>。Compass では<a href="http://compass-style.org/reference/compass/typography/vertical_rhythm/">タイポグラフィ ヘルパー</a>を使用して、ページの縦のリズムを作成して管理したり、リストの管理、およびリンクのスタイル設定も簡単に行えます。</li>
	<li><strong>プラグインその他</strong>。<a href="https://github.com/chriseppstein/compass/wiki/Compass-Plugins">コミュニティ プラグイン</a>のリストはますます大きくなり、さまざまなプロジェクトで使用するスタイルを簡単にパッケージ化できます。</li>
</ul>
<h3 id="installation">インストール</h3>
Compass をアセット パイプライン内で使用するには、Gemfile 内のアセット グループに Compass バージョン <code>0.11.0</code> (または勇気のある方は edge) を追加してください。
<pre escaped="true">group :assets do
  gem 'sass-rails',   '~&gt; 3.1.4'
  gem 'coffee-rails', '~&gt; 3.1.1'
  gem 'uglifier',     '&gt;= 1.0.3'
  gem 'compass',      '~&gt; 0.11.0'
end</pre>
gem バンドルを更新すると、Compass mixin をスタイルシートで使用できるようになります。
<h3 id="changesforcompassusers">Compass ユーザーを対象とした変更点</h3>
Rails 3.1 以前に Compass を使用していた場合、アセット パイプラインでの Compass 使用にあたって注意の必要な変更がいくつかあります。

<strong>バンドル オプションを選択する。</strong>まず、Sprockets でスタイルシート バンドルを管理するか、Sass の partial を使用するかを決定します。Sass ファイルで Sprockets manifest の <code>require</code> と <code>include</code> ディレクティブを使用できますが、スタイルシートに CSS アセットを含めるというもっと簡単な方法もあります。<code>.scss.</code> ファイル拡張子を使って CSS ファイルの名前を変更すると、メイン スタイルシートでインデント構文と <code>.sass</code> 拡張子を使用する場合でも、その CSS ファイルを partial として Sass スタイルシートで使用できます。

<strong>アセットの場所に注意する。</strong>Compass ヘルパーの <code>image-url</code> や <code>font-url</code> などを使用する場合、これらのヘルパーが <code>/images</code> や <code>/fonts</code> の代わりに <code>/assets</code> で解決される点に注意してください。したがって、イメージとフォントは <code>public</code> フォルダー内の以前の場所ではなく、それぞれ <code>app/assets/images</code> と <code>app/assets/fonts</code> に保存する必要があります。
<h2 id="optimizingfordevelopment">開発用の最適化</h2>
アセット パイプラインには多彩な機能がありますが、これには代償が伴います。最大の問題点は処理速度です。アセット パイプラインでは各アセット要求ごとに <em>Rails スタック全体</em>が読み込まれます。これは、小さなアプリケーションでは問題になりません。しかし、多くの gem 依存関係がある大規模なアプリケーション (特に Rails エンジンを使用したもの) は、開発環境で要求ごとに多数のクラスを読み込み直すため、パイプライン経由のアセットのレンダリングにかかる時間がずっと長くなる可能性があります。
<h3 id="tweakyoursetup">セットアップの調整</h3>
アセットのコンパイルが遅いためフロントエンドの開発がスローダウンする場合は、<a href="http://wavii.com/">Wavii</a> 提供の gem <a href="https://github.com/wavii/rails-dev-tweaks">rails-dev-tweaks</a> の使用を検討します。この gem には Rails の自動読み込み規則を変更する機能があるので、開発中の各要求間の再読み込みが回避されます。既定の規則では、アセット、XHR、および favicon 要求でのクラスの再読み込みをスキップします
<pre escaped="true">config.dev_tweaks.autoload_rules do
  keep :all

  skip '/favicon.ico'
  skip :assets
  skip :xhr
  keep :forced
end</pre>
スピードがアップしますが、カスタムの Sass 関数を使用している場合、これらの変更を確認するにはサーバーをバウンスする必要があります。
<h3 id="precompileengineassets">エンジン アセットのプリコンパイル</h3>
本番と同じようにアセットをプリコンパイルして、アセット パイプラインを回避することにより、開発環境の処理速度を大きく上げることができます。この方法はスタイルシートに変更を加えないチーム メンバーには向いていますが、スタイルシートの作成者にはあまり役に立ちません。これには Rails エンジンという大きな例外があります。

Devise、Spree、Refinery といった Rails エンジンにはパワフルな機能があります。gem を設定してジェネレーターを実行するだけで、それほど手間をかけずに認証、ストアフロント、または CMS 機能などを Rails アプリケーションに追加できます。アプリケーションがエンジンを使用して開発環境の速度が大きく低下する場合には、エンジン アセットがパイプラインに負荷をかけていないか確認してください。<a href="http://spreecommerce.com">Spree</a> の場合は、Rails の rake タスクでアセットをプリコンパイルして<a href="http://guides.spreecommerce.com/getting_started.html#improving-performance">アセットのパフォーマンスを改善</a>することができます。
<pre escaped="true">rake assets:precompile RAILS_ENV=development RAILS_ASSETS_NONDIGEST=true</pre>
これによってすべてのアプリケーション アセットが /public/assets にコンパイルされ、Rails は各要求ごとに再コンパイルを行わずにこれらを提供できるようになります。
<pre escaped="true">drwxr-xr-x  17 wynn  staff   578 Nov  2 08:36 .
drwxr-xr-x   8 wynn  staff   272 Nov  2 08:35 ..
drwxr-xr-x  16 wynn  staff   544 Nov  2 08:36 admin
-rw-r--r--   1 wynn  staff   155 Nov  2 08:30 application.css
-rw-r--r--   1 wynn  staff   143 Nov  2 08:30 application.css.gz
drwxr-xr-x   7 wynn  staff   238 Nov  2 08:36 creditcards
drwxr-xr-x   3 wynn  staff   102 Nov  2 08:36 datepicker
-rw-r--r--   1 wynn  staff  1150 Nov  2 08:19 favicon.ico
drwxr-xr-x   6 wynn  staff   204 Nov  2 08:36 icons
drwxr-xr-x   4 wynn  staff   136 Nov  2 08:36 jqPlot
drwxr-xr-x  15 wynn  staff   510 Nov  2 08:36 jquery-ui
drwxr-xr-x   3 wynn  staff   102 Nov  2 08:35 jquery.alerts
drwxr-xr-x   3 wynn  staff   102 Nov  2 08:35 jquery.jstree
-rw-r--r--   1 wynn  staff  6694 Nov  2 08:36 manifest.yml
drwxr-xr-x   5 wynn  staff   170 Nov  2 08:36 noimage
-rw-r--r--   1 wynn  staff  1608 Nov  2 08:19 spinner.gif
drwxr-xr-x   6 wynn  staff   204 Nov  2 08:36 store</pre>
アセットをプリコンパイルすることで読み込み時間は大幅に削減されますが、自分のスタイルシートには変更がありません。上の例で <code>application.css</code> と <code>application.css.gz</code> を削除して、これらが各要求ごとにアセット パイプライン経由でコンパイルされるようにできます。しかし、エンジンによって提供されるスタイルシートをプリコンパイルすると、大きな変化が得られます。

すでに説明したように、アセット パイプラインにはスタイルシートを連結してファイルの数を少なくできるという大きな利点があります。アプリケーション固有の複数のスタイルシートを提供する場合、すべてのアセットをまずプリコンパイルしてから、現在作業中のスタイルシートを /public/assets から削除することを検討してください。
