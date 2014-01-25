---
layout: post
status: publish
published: true
title: Engine Yard Cloud上のPHPにOpenPNE3(symfony1.4)をデプロイ
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1044
wordpress_url: http://www.engineyard.co.jp/blog/?p=1044
date: 2013-05-09 12:35:33.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/MySNS-1.png" alt="MySNS-1" width="942" height="613" class="alignnone size-full wp-image-1046" />

Engine Yard Cloud上にオープンソースのプロダクトをデプロイする実例として今回はsymfony1.4で構築されたソーシャルネットワーク構築ソフトウェアとして知られている<a href="http://www.openpne.jp/" target="_blank">OpenPNE3</a>をデプロイしてみます。OpenPNEは2004年から<a href="http://www.tejimaya.com/" target="_blank">手嶋屋</a>さんが開発されている実績あるソフトウェアで3万を超えるさまざまな団体やサイトでコミュニティ機能を構築する為に利用されています。またプラグインを利用してさまざまな機能を拡張できるのが特徴です。

またフレームワークとしてsymfony1.4を利用して様々な機能を実装しており、ソフトウェアの構造が洗練されているのも特徴です。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/OpenPNE_プラグイン｜OpenPNE.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/OpenPNE_プラグイン｜OpenPNE-1024x842.png" alt="OpenPNE_プラグイン｜OpenPNE" width="1024" height="842" class="alignnone size-large wp-image-1348" /></a>

<h3>デプロイの手順</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/Engine-Yard-Cloud-—-Apps.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/Engine-Yard-Cloud-—-Apps.png" alt="Engine Yard Cloud — Apps" width="513" height="473" class="alignnone size-full wp-image-1054" /></a>

OpenPNEはコードの展開後にsymfonyコマンドを利用したタスクを起動してインストールを行います。この部分の手順を<a href="https://github.com/yandod/OpenPNE3" target="_blank">デプロイフックを利用して自動化したリポジトリ</a>を作成しました。アプリケーションの実行言語にはPHPを選択し、リポジトリには<code>git://github.com/yandod/OpenPNE3.git</code>を指定し、またドキュメントルートはsymfonyの標準である<code>web/</code>に設定します。

あとはデータベースにMySQLを設定し、お好きな構成でサーバを起動します。（なお今月から価格改定があり<strong>スモールインスタンスが1時間あたり8円(30日で5760円)</strong>と大変オトクになっています。サーバが起動したらデプロイ対象のリビジョンに<code>engineyard</code>ブランチを指定してデプロイを行います。

<h3>デプロイフックの内容</h3>
<pre lang="ruby">
if !Dir.exist?(shared_path + "/config/OpenPNE.yml") then
  run "cp #{release_path}/config/OpenPNE.yml.sample #{shared_path}/config/OpenPNE.yml"
  run "cp #{release_path}/config/ProjectConfiguration.class.php.sample #{shared_path}/config/ProjectConfiguration.class.php"
end

# prepare shared files
run "cp #{shared_path}/config/OpenPNE.yml #{release_path}/config/OpenPNE.yml"
run "cp #{shared_path}/config/ProjectConfiguration.class.php #{release_path}/config/ProjectConfiguration.class.php"

# set timezone in php.ini
sudo "echo 'date.timezone = Asia/Tokyo' > /etc/php/cgi-php5.4/ext-active/timezone.ini"
sudo "echo 'date.timezone = Asia/Tokyo' > /etc/php/cli-php5.4/ext-active/timezone.ini"
sudo "echo 'date.timezone = Asia/Tokyo' > /etc/php/fpm-php5.4/ext-active/timezone.ini"

# set allow_url_fopen = On
sudo "echo 'allow_url_fopen = On' > /etc/php/cgi-php5.4/ext-active/allow_url.ini"
sudo "echo 'allow_url_fopen = On' > /etc/php/cli-php5.4/ext-active/allow_url.ini"
sudo "echo 'allow_url_fopen = On' > /etc/php/fpm-php5.4/ext-active/allow_url.ini"

run "curl https://gist.github.com/yandod/5539221/raw/a66946162ac1ba2e9d59f89cca508ea2cadae477/custom.conf | sed -e 's/openpne3/#{app}/' > /data/nginx/servers/#{app}/custom.conf"

run "./symfony openpne:fast-install --dbms=mysql --dbuser=deploy --dbpassword=#{node['users'][0]['password']} --dbhost=#{node['db_host']} --dbname=#{app}"
run "./symfony project:clear-controllers"
</pre>

<a href="https://github.com/yandod/engineyard-openpne-deploy" target="_blank">今回のデプロイフック</a>はフレームワークにsymfonyを利用している事もありかなりスムーズな内容になりました。設定ファイルを共通ディレクトリ<code>/data/#{app}/shared</code>に作成してからデプロイ毎に作成されるディレクトリ<code>/data/#{app}/releases/</code>にコピーしています。Capistranoのディレクトリ構造と共通のこの構造を利用して設定ファイルなどを配置するのはEngine Yardを利用する際の基本的なテクニックです。
あとはインストーラーを起動してインストールを行なっています。また末尾のコマンドでは運用時には不要なコントローラーの削除を行っています。必要であればさらにOpenPNEのプラグインをインストールするコマンド(例えば <code>./symfony opPlugin:install opCommunityTopicPlugin</code> など)を追加しても良いでしょう。

<h3>OpenPNE3 + Engine YardでスケーラブルなSNSを</h3>
これでインストールは完了です。OpenPNEはデータベースのスケールアウトなどにも対応しており、必要に応じてスケールアウトした構成で動作させる事もできます。またメールの送信を行うのであればメール送信用のアドオン、SendGridを有効にしてOpenPNE.ymlにメールサーバの設定内容をしたり、死活監視が必要であればEngine Yardのダッシュボードから監視用URLを設定してください。この設定を行う事で2分ごとに設定されたURLの応答をEngine YardがチェックしHTTPエラーが発生していた場合はアラートを送信します。またアラートの内容についてはEngine Yardのサポートエンジニアが24時間体制で監視しています。

スケーラブルなSNSの運用環境やsymfonyアプリケーションの運用環境の選択肢としてEngine Yard Cloudを検討する材料になればと思います。

<div style="text-align:center"><a href="http://www.engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" style="border: 1px solid black"></a></div>
