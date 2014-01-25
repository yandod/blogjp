---
layout: post
status: publish
published: true
title: RedmineをEngine Yard Cloudに自動デプロイ
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 657
wordpress_url: http://www.engineyard.co.jp/blog/?p=657
date: 2013-03-12 16:16:06.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/03/チケット-Test-Project-Redmine.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/03/チケット-Test-Project-Redmine-1024x637.jpg" alt="チケット - Test Project - Redmine" width="1024" height="637" class="alignnone size-large wp-image-658" /></a>

PaaS環境は独自に開発したアプリケーションを稼働させる環境として利用される事も多いですが、オープンソースなどの既存のプロダクトをセットアップして動作させる環境としても利用できます。今回はRailsで実装された人気のバグ管理システムであるRedmineをEngine Yard Cloud上にセットアップしてみました。

通常、Redmineのインストール時に手動で実行する手順の自動化や、Gemfileの<a href="https://github.com/yandod/example-redmine" target="_blank">微調整を行ったRedmine</a>を作成してみました。このソースコードを利用すれば一切、シェル上での作業などをする事なく自動的にRedmineをセットアップできます。
またEngine Yardの機能を利用したスケールアウトやスナップショット、バックアップの機構が利用できますのでこのまま運用するだけでかなりの信頼度でRedmineを運用できます。

下記の動画を見ていただくと数回のクリックだけでセットアップできているのが分かるかとおもいます。（インスタンスの作成時の待ち時間は編集してあります。）

<iframe width="640" height="480" src="http://www.youtube.com/embed/eAth6BSZVQA?rel=0" frameborder="0" allowfullscreen></iframe>

<h2>今回の対応で行った事</h2>
今回の対応でEngine Yard特有の対応を行なっている点は下記の２点です。

<ul>
<li>rmagickのバージョンをGemfile上で固定</li>
<li>インストール時に必要なシェル作業の自動化</li>
</ul>

Engine Yardにデフォルトで導入されているImage Magickの場合はrmagickは2.12.2となります。Image Magick自体をアップグレードするクックブックを書けば最新を使う事もできますが、まずは問題のないバージョンを利用する形にしてあります。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/03/freeze-version-of-rmagick-for-Engine-Yard-·-b437c8a-·-yandod_example-redmine.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/03/freeze-version-of-rmagick-for-Engine-Yard-·-b437c8a-·-yandod_example-redmine.jpg" alt="freeze version of rmagick for Engine Yard · b437c8a · yandod_example-redmine" width="936" height="330" class="alignnone size-full wp-image-667" /></a>

インストール時に必要な作業についてはEngine Yardのデプロイフックと呼ばれる機構で呼び出されるスクリプトから実行します。
これによりインスタンス起動時やデプロイ時に任意の処理を行えます。

<strong>deploy/before_migrate.rb</strong>
<pre lang="ruby">
rakecmd = 'rake'
if !File.exist?("/usr/bin/rake") then
  rakecmd = 'rake19'
end

if !File.exist?("#{shared_path}/config/secret_token.rb") then
  run "bundle install"
  run "#{rakecmd} generate_secret_token"
  run "mv #{release_path}/config/initializers/secret_token.rb #{shared_path}/config/secret_token.rb"
end

run "ln -s #{shared_path}/config/secret_token.rb #{release_path}/config/initializers/secret_token.rb"
</pre>

<h2>課題</h2>
ひとまず動作するようになっていますが、現時点では下記の問題があると予想しています。

<ul>
	<li>Redmineの安定版などに対する随時対応</li>
	<li>Ruby1.9対応</li>
</ul>

今回のパッチはRedmineの公式のブランチ運用やリリースサイクルは考慮せずにmasterに対してフォークしています。修正内容はとても小さいのでバッティングする可能性は低いので同様の修正を利用したいバージョンのRedmineに対してかければ良いでしょう。
またRuby1.9でもデプロイはできますが、メールのテンプレート関係のところでエンコーディングのエラーが発生しています。この点には今回は対応していません。

