---
layout: post
status: publish
published: true
title: APIを使ってインスタンスの追加削除が行えます
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 468
wordpress_url: http://www.engineyard.co.jp/blog/?p=468
date: 2013-01-24 17:41:49.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/01/Twitter-_-jlehrbaum_-Like-to-get-freaky-with-the-....jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/01/Twitter-_-jlehrbaum_-Like-to-get-freaky-with-the-...-300x246.jpg" alt="" title="Twitter _ jlehrbaum_ Like to get freaky with the ..." width="300" height="246" class="alignnone size-medium wp-image-469" /></a>

通常、アプリケーションサーバーなどのインスタンスの増減はダッシュボード上の操作で行います。Engine Yard Cloudにはアーリーアクセス機能としてAPIが提供されておりこのAPIを通じてインスタンスのコントロールを行う事もできます。こちらの情報はブログではなく<a href="https://twitter.com/jlehrbaum/status/292120153083240448" target="_blank">Twitterで告知されていました</a>。

<strong>セキュリティ</strong>
Engine Yard Cloud API v2はAPIトークンとHTTPSを利用して認証を行います。2要素認証は現在のところサポートしていません。

<strong>利用の流れ</strong>
ダッシュボードにログインし、「Early Access」のセクションから「Add/Remove Instances API」を有効化します。またAPIトークンを入手するためにengineyardのgemをインストールします。gemをインストール後にローカルファイルからAPIトークンを確認します。

<pre>
ey login 
cat ~/.eyrc 
---
api_token: 76f2d43d79bedd9bc74654a1ded733c9
</pre>

<strong>Environmentの情報の確認</strong>
インスタンスの増減を行うにはEnvironmentのIDを指定する必要があります。IDについてはAPIトークンを使って下記のように取得できます。<a href="https://support.cloud.engineyard.com/entries/22895198-get-environment-data" target="_blank">参考記事</a>

<pre>
GET https://cloud.engineyard.com:443/api/v2/environments
</pre>

レスポンスはJSONで下記のように返却されます。
<pre>
{
 "environments": [{
 "id": 44444,
 "name": "enviro_new_todo",
 "ssh_username": "deploy",
 "app_server_stack_name": "nginx_passenger3",
 "framework_env": "production",
 "instance_status": "none",
 "instances_count": 0,
 "load_balancer_ip_address": "50.112.999.999",
 "account": {
 "id": 11111,
 "name": "my-1st-trial"
 },
 "stack_name": "nginx_passenger3",
 "instances": [],
 "app_master": null,
 "apps": [{
 "id": 22222,
 "name": "app_myown_todo",
 "repository_uri": "git://github.com/engineyard/todo.git",
 "app_type_id": "rails3",
 "account": {
 "id": 11111,
 "name": "my-1st-trial"
 }
 }],
 "deployment_configurations": {
 "app_myown_todo": {
 "id": 55555,
 "domain_name": "_",
 "uri": null,
 "migrate": {
 "perform": true,
 "command": "rake db:migrate"
 },
 "name": "app_myown_todo",
 "repository_uri": "git://github.com/engineyard/todo.git"
 }
 }
 }]
}
</pre>

<strong>インスタンスの追加</strong>
EnvironmentのIDが分かればアプリケーションサーバかユーティリティサーバに対してノードの追加を行えます。パラメータとしてインスタンスの種別やサイズ、稼働するアベイラビリティゾーンを指定して下記のエンドポイントを呼び出します。<a href="https://support.cloud.engineyard.com/entries/22547223-add-an-instance" target="_blank">参考記事</a>

<pre>
POST https://cloud.engineyard.com:443/api/v2/environments/YOUR_ENVIRO_ID_GOES_HERE/add_instances
</pre>

レスポンスとしては下記のようなJSONが返却されます。

<pre>
{
 "request": 
 {
 "role": "util",
 "name": "foo"
 },
 "instance": 
 {
 "amazon_id": null,
 "availability_zone": null,
 "bootstrapped_at": null,
 "chef_status": null,
 "error_message": null,
 "id": 999999,
 "name": "foo",
 "role": "util",
 "size": "medium_cpu",
 "status": "starting",
 "public_hostname": null,
 "private_hostname": null
 },
 "status": "accepted"
}
</pre>


現在のところオートスケールなどはサポートしていないEngine Yard Cloudですが、APIを利用したインスタンスの増減を利用する事で必要な際にインスタンスを増やしたり、夜間はインスタンスを減らしてコストを削減するといった対応が実装できます。

また現在のところデータベースインスタンスについてはAPIからの追加、削除はできない点にご注意ください。

参考ドキュメント
<a href="https://support.cloud.engineyard.com/entries/22498973-use-the-instance-provisioning-api-with-engine-yard-cloud">Use the Instance Provisioning API with Engine Yard Cloud : Engine Yard Developer Center</a>
