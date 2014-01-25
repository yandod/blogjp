---
layout: post
status: publish
published: true
title: 'Composerを活用したモダンな開発手法をPHPカンファレンス2013で発表してきた。 #phpcon2013'
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1471
wordpress_url: http://www.engineyard.co.jp/blog/?p=1471
date: 2013-09-17 15:50:42.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/203130914_Composer.001.png" alt="203130914_Composer.001" width="1024" height="768" class="alignnone size-full wp-image-1473" />

2013/9/14に蒲田の太田区産業プラザPiOで開催されたPHPカンファレンス2013でComposerについての発表を行ってきました。Composerを使った事が無い方向けにまずComposerを使うと何が便利なのか、autoloadがどのように便利かという点に絞って解説をさせて頂きました。発表資料は下記です。既にComposerを使っている方々にとっては聞き飽きた情報かもしれませんが、これからComposerを使う人に向けて改めてポイントを振り返ります。

<script async class="speakerdeck-embed" data-id="0bf726a0018a0131a9f86e64ddb58d77" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

<h3>Composerは今すぐに使える</h3>
<pre lang="javascript">
{
    "require": {
        "dg/twitter-php": "*"
    },
    "autoload": {
        "psr-0": {"": "lib/"}
    }
}
</pre>
ComposerはPHPのコマンドラインが使える環境であれば簡単に実行できます。インストーラーを実行すればPHPから実行可能な composer.phar を手元にダウンロードできますのでそれを実行するだけです。リポジトリには<code>composer.json</code>と<code>composer.lock</code>のみをコミットしておき、ステージング環境や本番環境などでそれぞれ<code>composer install</code>を実行すれば同じソースが再現されます。Engine YardのようなPaaS環境では<code>composer.json</code>を自動で検出してインストールを行いますので特にデプロイの手順を検討しなくても大丈夫です。
df/twitter-phpを使ったサンプルであれば上記の<code>composer.json</code>を作成し、<code>composer install</code>するだけで準備完了です。

<h3>Composerの提供するautoloadがとても便利</h3>
<pre lang="php">
<?php
// autoload.php の読み込み
require_once 'vendor/autoload.php';

//Twitterクラスが自動で読み込まれる
$twitter = new Twitter(
    'aaaaa',
    'bbbbbb',
    'ccccc-ccccc',
    'dddddddd'
);

//MyClassも自動で読み込まれる
$obj = new MyClass();
var_dump($obj->test());

$info = $twitter->loadUserInfo('yando');
var_dump($info->status->text);
$twitter->send('Composerは便利、絶対使おう！ #phpcon2013');
</pre>
Composerで導入したライブラリはオートロードのサポートを受ける事が出来ます。これにより複雑なディレクトリ構造などを考慮する事なく、必要なクラスが必要な時にだけ読み込まれるようになります。Composerを使うようになれば、<code>require_once</code>をアプリケーションの実装中に書くことは最初に<code>autoload.php</code>を読み込む時の1回だけで済みます。

<h3>CakePHPや既存のアプリとの共存も可能</h3>
Composerは既存のアプリケーションやフレームワークと組み合わせる事もできます。Composerがデフォルトで利用するVendorディレクトリにすでに何かが存在してれば、設定で名前を変更すれば既存のコードを壊すことなくライブラリの導入ができます。ソースコードに直接添付されたライブラリを少しづつ減らしてComposerで導入したライブラリに乗り換えていけば移行ができます。

Composerを利用する事で手動でコピーされたライブラリの改変やアップデートの停滞などの悪習を減らし、手間を少なくしつつ品質を上げる事ができます。まだComposerを利用していないあらゆるPHP5.3以上のプロジェクトでぜひとも導入を検討してみたください。
<hr>

Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。Composerを利用したアプリケーションをデプロイする際は、Engine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/trial"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>
