---
layout: post
status: publish
published: true
title: Engine Yard Cloud上のPHPにDrupalをデプロイ
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 970
wordpress_url: http://www.engineyard.co.jp/blog/?p=970
date: 2013-04-24 19:04:12.000000000 +09:00
categories:
- Uncategorized
tags: []
comments:
- id: 38
  author: Engine Yard Cloud上のPHPにCandyCaneをデプロイ - Engine Yard Blog JP | Engine Yard
    Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/candycane-on-engineyard/
  date: '2013-04-26 16:42:39 +0900'
  date_gmt: '2013-04-26 07:42:39 +0900'
  content: '[...] Engine Yard Cloud上のPHPにDrupalをデプロイ Engine Yard CloudでPHPを利用できるようになりました
    [...]'
- id: 42
  author: Engine Yard で WordPress を動かす | dogmap.jp
  author_email: ''
  author_url: http://dogmap.jp/2013/05/02/wordpress-on-engine-yard/
  date: '2013-05-02 22:24:08 +0900'
  date_gmt: '2013-05-02 13:24:08 +0900'
  content: '[...] 先月辺りから、クラウド上へアプリケーションをデプロイできる PaaS Engine Yard で PHP が使えるようになってます。
    Engine Yard では、無料トライアルでも 500 時間使えるので安心ですね。 WordPress をインストールしたとかの情報があまり見つけられなかったので、ここに書いておきますね。
    # Drupal をインストールする方法は、安藤さんが書いてくれてます。 # Engine Yard Cloud上のPHPにDrupalをデプロイ &#8211;
    Engine Yard Blog JP | Engine Yard Blog JP [...]'
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Welcome-to-EY-Drupal-EY-Drupal.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Welcome-to-EY-Drupal-EY-Drupal-1024x659.png" alt="Welcome to EY Drupal | EY Drupal" width="1024" height="659" class="alignnone size-large wp-image-971" /></a>

<a href="http://www.engineyard.co.jp/blog/2013/php-beta-on-engineyard-cloud/" target="_blank">Engine Yard Cloud上でPHPが動作するようになった事をお知らせ</a>して以降、さっそくPHPのデプロイを試して頂いた方がDrupalを利用していました。今回、設定の手順やデプロイをスムーズにするスクリプトを書いたのでこれらを併せてDrupalを動作させる手順として記事にしようと思います。

<h3>アプリケーションの作成時の注意点</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Engine-Yard-Cloud-—-Apps-1.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Engine-Yard-Cloud-—-Apps-1-1024x725.png" alt="Engine Yard Cloud — Apps-1" width="1024" height="725" class="alignnone size-large wp-image-975" /></a>

アプリケーションの作成画面で設定すべき点はApplication LanguageにPHPを選択し、Drupalのリポジトリを指定します。公式のリポジトリをそのまま指定しても問題ありませんが、 今回は<a href="https://github.com/yandod/drupal" target="_blank">デプロイスクリプトを同梱したこちらのフォーク</a> (<code>git://github.com/yandod/drupal.git</code>) を指定しています。またドキュメントルートの設定は空白に変更します。Drupalではプロジェクトの直下にindex.phpが配置されていますのでこれで問題ありません。

<h3>環境の作成時の注意点</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Engine-Yard-Cloud-—-Environments-3.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Engine-Yard-Cloud-—-Environments-3-1024x836.png" alt="Engine Yard Cloud — Environments-3" width="1024" height="836" class="alignnone size-large wp-image-976" /></a>

ここでも選択すべき内容は殆どありません。任意の名前を環境に付け、データベースからMySQL5.5やPostgreSQLを選びます。なお<code>Add to Existing Environment</code>を使うと同一のサーバに複数のアプリケーションをデプロイできるのですがPHPのスタックではまだ動作が未確認ですので選択しないようにしてください。
リージョンについては無料トライアルではus-east限定ですが、有料アカウントでは日本を含む全てのAWSのリージョンが選択できます。

<h3>デプロイ</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Engine-Yard-Cloud-—-Environment-drupal_demo7-of-application-drupal-1.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Engine-Yard-Cloud-—-Environment-drupal_demo7-of-application-drupal-1-1024x657.png" alt="Engine Yard Cloud — Environment drupal_demo7 of application drupal-1" width="1024" height="657" class="alignnone size-large wp-image-981" /></a>

Engine Yardの環境は特に特殊の環境ではないのでそのままのソースコードでも動作は問題ありません。とはいえデプロイを行う度にデータベースの設定ファイルなどが巻き戻ってしまうのは運用時に支障があります。冒頭で示したフォークはデータベースの設定ファイルや画像ファイルなどのデプロイの際に持ち越すべきファイルを共通のディレクトリに移動してシムリンクを貼るようにしてあります。このスクリプトはengineyardブランチに入っていますので、このブランチを指定してデプロイを行なってください。

<a href="https://github.com/yandod/engineyard-drupal-deploy/blob/393f794084c184a21cf8e980b906b3f37164eca6/before_bundle.rb" target="_blank">ファイルを退避するデプロイスクリプト deploy/before_bundle.rb</a>
<pre lang="ruby">
# link sites directory
if !Dir.exist?(shared_path + "/sites") then
  run "cp -R #{release_path}/sites #{shared_path}/sites"
end
run "rm -Rf #{release_path}/sites && ln -s #{shared_path}/sites ./sites"

# set timezon in php.ini
#sudo "echo 'date.timezone = Asia/Tokyo' > /etc/php/cgi-php5.4/ext-active/timezone.ini"
#sudo "echo 'date.timezone = Asia/Tokyo' > /etc/php/cli-php5.4/ext-active/timezone.ini"
#sudo "echo 'date.timezone = Asia/Tokyo' > /etc/php/fpm-php5.4/ext-active/timezone.ini"
</pre>

<h3>データベースの接続設定</h3>
データベースの情報は環境変数に格納されています。しかしDrupalはこの情報を自動で読み取ってはくれないので<a href="https://support.cloud.engineyard.com/entries/22348236-%E3%82%A4%E3%83%B3%E3%82%B9%E3%82%BF%E3%83%B3%E3%82%B9%E3%81%B8%E3%81%AESSH-%E6%8E%A5%E7%B6%9A-Connect-to-Your-Instance-with-SSH-" target="_blank">インスタンスへSSHで接続</a>を行い設定ファイルに記載された接続情報を確認します。独自で実装したアプリケーションであればこのymlを読み込んで接続するようにしておけば自動的に接続できます。

<pre lang="cmd">
$ cat /data/drupal/shared/config/database.yml 

production:
  adapter:   mysql
  database:  'drupal'
  username:  'deploy'
  password:  '1111111'
  host:      'ec2-11-111-111-10.compute-1.amazonaws.com'
  reconnect: true
</pre>

一度デプロイが終わればシムリンクが貼られた<code>/data/drupal/shared/sites/default/setting.php</code>を環境変数を使った形に変更するのも良いでしょう。

<h3>Drupalの設定</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Choose-language-Drupal.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Choose-language-Drupal.png" alt="Choose language | Drupal" width="952" height="513" class="alignnone size-full wp-image-984" /></a>

あとはブラウザからアクセスすればDrupalの設定画面が表示されますので順次設定を行います。前述したデプロイスクリプトが含まれるブランチからデプロイされていれば、設定が完了した後にデプロイを行なってもサイトが初期状態に戻る事はなくコードの更新を行えます。CMSなどのシステムでは設定ファイルやプラグイン、画像ファイルなどを保持する必要がある事が多いのでデプロイスクリプトなどを使ってファイルの退避を行うのは基本的なテクニックになりますので是非覚えておいてください。

<div style="text-align:center"><a href="http://www.engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" style="border: 1px solid black"/></div></a>
