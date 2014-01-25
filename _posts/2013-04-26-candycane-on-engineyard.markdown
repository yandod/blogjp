---
layout: post
status: publish
published: true
title: Engine Yard Cloud上のPHPにCandyCaneをデプロイ
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1001
wordpress_url: http://www.engineyard.co.jp/blog/?p=1001
date: 2013-04-26 16:42:27.000000000 +09:00
categories:
- Uncategorized
tags: []
comments:
- id: 64
  author: CakeFest2013で発表されたCakePHP3の未来 | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/cakephp3-on-cakefest/
  date: '2013-09-04 22:34:58 +0900'
  date_gmt: '2013-09-04 13:34:58 +0900'
  content: '[...] Chef + VagrantによるPHP5.3 + MySQL + nginxの開発環境 Engine Yard Cloud上のPHPにCandyCaneをデプロイ
    CakeFest 2013 Photos #cakefest @cakephp | [...]'
---
前回は世界的に利用されているCMS,Drupalをデプロイしてみましたが、今回はRedmineをCakePHPに移植したバグ管理システム CandyCaneをデプロイしてみます。CandyCaneは私自身が開発者ということもありデプロイ用のスクリプトをコアに同梱しました。インストールプロセスも自動化されているのでダッシュボードからのクリックのみで実際にタスク管理を始められます。
また作成したデプロイスクリプトはCakePHPを利用したプロジェクトであれば多少の修正で流用できますので、CakePHPのアプリケーションをクラウドに載せたい方にも参考になるでしょう。

<h3>アプリケーション作成時の設定</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Engine-Yard-Cloud-—-Apps-2.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/Engine-Yard-Cloud-—-Apps-2.png" alt="Engine Yard Cloud — Apps-2" width="977" height="604" class="alignnone size-full wp-image-1008" /></a>

CandyCaneをデプロイする場合は公開されているリポジトリのURL <code>git://github.com/yandod/candycane.git</code> をそのまま設定し、ドキュメントルートを<code>app/webroot/</code>に設定します。

<h3>環境の設定</h3>
CandyCaneはPostgreSQLにも対応していますが、今の段階ではインストールスクリプトはMySQLを想定していますので、MySQL5.5を選択します。サーバ構成についてはカスタム設定を選択してStandard Smallインスタンスなどを選択します。サーバーの台数も任意の台数でホスティングできます。(アプリケーションサーバを複数台構成にする場合は、添付ファイルやプラグインを複数サーバで同期させるには手動のスクリプト実行が必要になる点が注意事項です。)

下記のインストールスクリプトは自動的にCakePHPの設定ファイルを生成し、デプロイをしても保持されるディレクトリ<code>/data/{appname}/shared/</code>の下に配置してからシムリンクを貼っています。

<pre lang="ruby">
if !Dir.exist?(shared_path + "/app/Config") then
  run "mkdir -p #{shared_path}/app/Config/"
  run "cp #{release_path}/app/Config/core.php #{shared_path}/app/Config/core.php"
  run "echo \"<?php
  class DATABASE_CONFIG {
  	var \\\$default = array();
  	public function __construct()
  	{
  	  \\\$this->default = array(
    		'datasource' => 'Database/Mysql',
    		'persistent' => false,
    		'host' => \\\$_SERVER[\"DB_HOST\"],
    		'login' => \\\$_SERVER[\"DB_USER\"],
    		'password' => \\\$_SERVER[\"DB_PASS\"],
    		'database' => \\\$_SERVER[\"DB_NAME\"],
    		'prefix' => '',
    		'port' => '',
    		'encoding' => 'utf8',
    	);
  	}
  }\" > #{shared_path}/app/Config/database.php"
  run "mkdir -p #{shared_path}/app/files/"
  run "mkdir -p #{shared_path}/app/Plugin/"
  run "mysql #{app} < #{release_path}/app/Config/sql/mysql.sql"
end

# prepare shared files and directories
run "rm #{release_path}/app/Config/core.php && ln -s #{shared_path}/app/Config/core.php #{release_path}/app/Config/core.php"
run "ln -s #{shared_path}/app/Config/database.php #{release_path}/app/Config/database.php"
run "ln -s #{shared_path}/app/Plugin #{release_path}/app/Plugin"
run "ln -s #{shared_path}/app/files #{release_path}/app/files"
</pre>

<h3>起動、動作確認</h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/ホーム.png" alt="ホーム" width="894" height="413" class="alignnone size-full wp-image-1027" />
あとはインスタンスが起動すれば自動的にデータベース接続の設定が行われ初期インストールまで自動で行います。あとはそのままユーザ名、パスワードそれぞれ<code>admin</code>でログインできます。ダッシュボードから再び最新版をデプロイした場合も設定ファイルやプラグイン、添付ファイルは保持したまま最新版にアップデートできるようになっています。

またパフォーマンスを向上させる為にAPCを導入もしてみます。APCを導入するにはSSHで接続し下記のコマンドを実行します。

<pre lang="cmd">
sudo pecl install apc
sudo sh -c "echo 'extension=apc.so' > /etc/php/cli-php5.4/ext-active/apc.ini'"
sudo /etc/init.d/php-fpm restart
</pre>

<h3>Engine Yard CloudのPHPによって提供される機能</h3>
Engine Yard Cloudを利用する事によって自動的に設定される機能は下記のようなものがあります。

<ul>
<li>ストレージデータのスナップショット(デプロイ、再起動などのタイミング)</li>
<li>データベースデータの定時バックアップ<br/><a href="https://support.cloud.engineyard.com/entries/22347703">データベースのバックアップ : Engine Yard Developer Center</a></li>
<li>指定したURLの24時間死活監視とEメールアラート<br/><a href="https://support.cloud.engineyard.com/entries/22328413">アプリケーションの監視 (Set up application monitoring) : Engine Yard Developer Center</a></li>
</ul>

個人的には死活監視と自動バックアップがとても便利だなと思っています。導入が簡単であってもバックアップなどが設定されていないといざという時に手痛い体験をする事になりますが、サボってしまいがちなのも事実。そういう意味で自動で処理してくれるというのはめんどくさがりのエンジニアにとっては良いですね。

<h3>関連する記事</h3>
<a href="http://www.engineyard.co.jp/blog/2013/drupal-on-engine-yard/" title="Engine Yard Cloud上のPHPにDrupalをデプロイ">Engine Yard Cloud上のPHPにDrupalをデプロイ</a>
<a href="http://www.engineyard.co.jp/blog/2013/php-beta-on-engineyard-cloud/" title="Engine Yard CloudでPHPを利用できるようになりました">Engine Yard CloudでPHPを利用できるようになりました</a>

<div style="text-align:center"><a href="http://www.engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" style="border: 1px solid black"/></a></div>
