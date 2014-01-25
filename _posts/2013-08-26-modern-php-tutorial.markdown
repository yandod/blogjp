---
layout: post
status: publish
published: true
title: モダンPHPチュートリアルを開催しました
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1412
wordpress_url: http://www.engineyard.co.jp/blog/?p=1412
date: 2013-08-26 14:28:00.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/08/DSC04859.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/08/DSC04859-1024x682.jpg" alt="DSC04859" width="1024" height="682" class="alignnone size-large wp-image-1414" /></a>

2013/8/24に開催された <a href="http://ll.jus.or.jp/2013/" target="_blank">LLまつり</a> にて「モダンPHPチュートリアル」というタイトルのチュートリアルを担当しました。内容としてはPHPをあまり追いかけていないような方にComposerを中心とした現在よく利用されている開発手法と、PHPのバージョンアップに伴い廃止された機能などを紹介しました。

<h3>古くなったプラクティス</h3>

古くなったプラクティスとしてはレガシー化したコードによく現れる特徴や、最新のPHPでは利用できなくなった、あるいは今後利用できなくなる項目として下記を挙げています。

<ul>
<li>ファイルの末尾の ?&gt;</li>
<li>拡張子 .inc のファイル</li>
<li>CR+LF (PSRにてPHPの改行コードはLFが推奨されました。)</li>
<li>register_globals(廃止済み)</li>
<li>safe_mode(廃止済み)</li>
<li>magic_quote(廃止済み)</li>
<li>@(例外処理を使うべき)</li>
<li>var(public private staticを使うべき)</li>
<li>=&(オブジェクトは標準で参照になるので不要)</li>
<li>mysql_connect(廃止予定)</li>
<li>require_once(autoload機構を利用すれば不要)</li>
<li>PEAR(最新版への更新が出来ない状態で改変されてしまいやすい)</li>
</ul>

PEARについてはやや誤解を招く表現になってしまいましたが、<strong>PEARを使ってはいけないという事ではありません。</strong>問題はアプリケーション内にコピーされ、さらに改変されてしまってアップデート不可能になってしまっているようなPEARです。PEARコマンドが標準でシステム全体のライブラリを変更してしまう事やinclude_pathの関係でアプリケーション内にPEARをコピーし、さらに改変を加えてしまっているケースはけっして少なくないでしょう。後述するComposerを使えば<strong>PEARのライブラリをより運用しやすい形で導入する事ができます</strong>。

<h3>新しいプラクティス</h3>
<script async class="speakerdeck-embed" data-id="175ad670eea3013085e85eb4ea32459d" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;">
<strong>PHPのベストプラクティス”The Right Way”の資料 #phpstudy</strong>
<a href="http://www.engineyard.co.jp/blog/2013/php-the-right-way/">http://www.engineyard.co.jp/blog/2013/php-the-right-way/</a>
</p>

新しい手法についてはPHP The Right Wayに読んで実践すればOKといって差し支えありません。その中でも核になりうるツールがComposerではないでしょうか。Composerを使えば下記のような事が可能になります。

<ul>
<li>PEARやSymfony、CakePHP、PHPUnit、Smartyなどのライブラリを自動でインストール</li>
<li>autoloadによりrequire_onceを書かずに全てのライブラリを利用可能</li>
<li>composer.jsonとcomposer.lockを同梱するだけでさまざまな環境で同じライブラリを自動セットアップ</li>
</ul>

Composerを使う事でソースコードから無駄なrequire_onceなどを書く必要が無くなりライブラリの利用や拡張が簡単になります。これまでのようにPEARのソースコードを書き換えてしまうような誘惑も減るでしょう。
またライブラリ本体はそもそもリポジトリにはコミットせず、設定ファイルから都度セットアップされるようになります。これもまたライブラリを直接改変してしまう事態を防いでくれます。あまり知られていないと思いますが、ComposerはPEARやSmarty、CakePHPなどをセットアップする事もできます。Composerからセットアップする事でautoloadの恩恵も受けやすくなります。

<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;">
<strong>CakePHPをComposerで導入する手順(Vagrantでのデモ環境同梱)</strong>
<a href="http://www.engineyard.co.jp/blog/2013/install-cakephp-on-composer/">http://www.engineyard.co.jp/blog/2013/install-cakephp-on-composer/</a>
</p>

<h3>Engine YardもComposerに対応</h3>
Engine YardのようなPaaSではアプリケーション内のcomposer.jsonを検出してライブラリのセットアップを自動的に行います。みなさんのリポジトリには本当に皆さんが書いたソースコードだけが含まれるようになりますので、開発時のソースコードが取り扱いやすくなります。

<hr>
Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。PHPを利用したアプリケーションをデプロイする際は、Engine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/trial"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>
