---
layout: post
status: publish
published: true
title: Engine Yard Cloud上のPHPでComposerとAPCをサポートしました
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1167
wordpress_url: http://www.engineyard.co.jp/blog/?p=1167
date: 2013-07-01 19:14:12.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/07/Composer.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/07/Composer.png" alt="Composer" width="605" height="427" class="alignnone size-full wp-image-1168" /></a>

PHPのアプリケーションの動作例が日を追うごとに増えているEngine Yard Cloudですが、PHP向けの機能が2つ追加されました。それがComposerとAPCです。どちらも実戦的なPHPアプリケーションの開発と運用には欠かせないツールですのでぜひお試しください。

<h2>Composerを使った依存関係の管理</h2>
Composerはアプリケーションが利用している外部のライブラリの管理やインストール、アップデート、読み込みを自動化する近代的なPHPアプリケーションには欠かせないツールです。ファイルの集合体であるPHPのライブラリはダウンロードして自分で配置したり、リポジトリにまるごと含めても動作はしますが、Composerを利用する事で下記のような利点が得られます。

<ul>
<li>リポジトリ内に外部のライブラリを同梱しないで良いのでコンパクトになる</li>
<li>外部ライブラリのインストール、最新版へのアップデートなどがコマンド一発で行える</li>
<li>セットアップしたライブラリのrequireをautoloadで自動化する</li>
</ul>

Composerを利用したアプリケーションの作り方は簡単です。composer.jsonに依存関係を記述し、アプリケーションからはautoload.phpだけをrequireするだけです。サンプルのコードを下記のリポジトリで公開しています。

<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;"><strong>Composerを利用したアプリケーションのサンプル</strong><br>
<a href="https://github.com/yandod/composer-sample" target="_blank">https://github.com/yandod/composer-sample</a></p>

今回はPackgist上で見つけたGitHubのAPIを利用するライブラリを使っています。composer.jsonに記述する内容は<a href="https://packagist.org/packages/knplabs/github-api" target="_blank">ページ上にかかれた内容</a>をコピーすれば大丈夫です。<code>composer install</code>を実行する事でこのライブラリやこのライブラリが利用しているその他のライブラリが自動的にインストールされます。

<pre lang="json">
{
    "name": "yandod/composer-sample",
    "require": {
        "knplabs/github-api": "~1.2@dev"
    }
}
</pre>

実際のアプリケーションではセットアップしたライブラリを使う際にrequireなどを何度も書く必要はありません。一度だけ、autoload.phpを読みこめばその他のライブラリの読み込みはPHP5のオートロード機構を使って必要な時に自動的に実行されます。

<pre lang="php">
<?php
require '../vendor/autoload.php';

$client = new Github\Client();
$repositories = $client->api('user')->repositories('yandod');
?>
<ul>
<?php foreach ($repositories as $row): ?>
<li><?php echo $row['name']; ?> (<?php echo $row['watchers'];?>) </li>
<?php endforeach; ?>
</ul>
</pre>

Engine Yard Cloudではcomposer.jsonがリポジトリに含まれている場合は自動的にcomposer installを実行して依存ライブラリのダウンロードを行います。この際にcomposer.lockも含まれているとインストールされるライブラリのバージョンを固定できます。デプロイの際に想定しないバージョンのライブラリがインストールされないようにcomposer.lockファイルもリポジトリにコミットしておくのが望ましいでしょう。
Composerによるインストールが自動的に行われた場合、Engine Yard Cloudのデプロイのログには下記のような情報が表示されます。

<pre lang="cmd">
+    03s  ~> Installing composer packages (composer.lock detected)
deploy@ec2-54-235-71-5.compute-1.amazonaws.com 'sh -l -c '\''composer install --no-interaction --working-dir /data/gitbreak_deploy/releases/20130701091243'\'
Loading composer repositories with package information
Installing dependencies (including require-dev) from lock file
- Installing kriswallsmith/buzz (v0.10)
Downloading: connection...    Downloading: 100%         
- Installing knplabs/github-api (dev-master 82b1a54)
Cloning 82b1a5407532323c8aa6bebff40c59de5604c806
Generating autoload files
</pre>

RubyやNodeなどで行われたいたように依存関係をプラットフォームが検出する事で運用の労力をさらに削減する事ができました。将来的には脆弱性が見つかっているライブラリを警告するといった挙動も実装されるかもしれません。


<h2>APCを使ったPHPの実行速度の向上とキャッシング</h2>
APCはPHPの実行速度を高速化する拡張モジュールです。従来は手動でPECLコマンドなどをインストールして導入する必要がありましたが、Engine Yard Cloudでは自動的に導入されるようになりました。APCは共有ホスティングなどの複数の開発者が利用する環境での利用には問題がありましたが、インスタンスを開発者が専有するEngine Yardではセキュリティ上の懸念もなく存分にその機能を利用できます。
フレームワークやCMSなどのコード量が多いアプリケーションでは特に効果が大きく、2倍以上のパフォーマンスが得られる場合もあります。またAPCにはキャッシュデータを保存する機能もあり、Memcacheのように利用することもできます。

Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。まだPHPのアプリケーションを自前の環境で動かしている方はこの機会にEngine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>



