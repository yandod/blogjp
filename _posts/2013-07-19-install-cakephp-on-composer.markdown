---
layout: post
status: publish
published: true
title: CakePHPをComposerで導入する手順(Vagrantでのデモ環境同梱)
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1226
wordpress_url: http://www.engineyard.co.jp/blog/?p=1226
date: 2013-07-19 20:42:06.000000000 +09:00
categories:
- Uncategorized
tags:
- 技術情報
- PHP
- CakePHP
comments:
- id: 61
  author: モダンPHPチュートリアルを開催しました | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/modern-php-tutorial/
  date: '2013-08-26 14:34:12 +0900'
  date_gmt: '2013-08-26 05:34:12 +0900'
  content: '[...] CakePHPをComposerで導入する手順(Vagrantでのデモ環境同梱) http://www.engineyard.co.jp/blog/2013/install-cakephp-on-composer/
    [...]'
- id: 62
  author: CakeFest2013で発表されたCakePHP3の未来 | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/cakephp3-on-cakefest/
  date: '2013-09-04 22:32:22 +0900'
  date_gmt: '2013-09-04 13:32:22 +0900'
  content: '[...] 2013 &#8211; a set on Flickr CakePHPをComposerで導入する手順(Vagrantでのデモ環境同梱)
    Chef + VagrantによるPHP5.3 + MySQL + nginxの開発環境 Engine Yard [...]'
- id: 72
  author: Composerを使ってみる | Hello, world!
  author_email: ''
  author_url: http://helloworld.525600.net/?p=1725
  date: '2013-10-08 16:15:01 +0900'
  date_gmt: '2013-10-08 07:15:01 +0900'
  content: '[...] CakePHPをComposerで導入する手順(Vagrantでのデモ環境同梱) [...]'
- id: 88
  author: gon
  author_email: t-m.i.mein-bebe-siees-auf@docomo.ne.jp
  author_url: ''
  date: '2013-11-20 14:05:00 +0900'
  date_gmt: '2013-11-20 05:05:00 +0900'
  content: |-
    失礼致します。
    質問というか相談になります。
    現在、CakePHPを導入をファイル転送で考えてますがうまくいきません。
    nginxを手動でCakePHPと連携させる方法はありますでしょうか？
- id: 89
  author: Yusuke Ando
  author_email: yando@engineyard.com
  author_url: ''
  date: '2013-11-20 15:59:00 +0900'
  date_gmt: '2013-11-20 06:59:00 +0900'
  content: |-
    申し訳ありませんが、仰っている状況が理解できていません。
    NginxとCakePHPは直接の関係はありませんので、まずはNginxでPHPが動作している状態を作り、その後にCakePHPのアプリケーションを導入することになるのではないでしょうか。
    Engine YardやVagrantをお使いになれば全ての設定は自動化されますので何もする必要はありません。

    環境や状況がわからないことには何かを申し上げる事はとてもむずかしいです。
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/07/cc.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/07/cc.png" alt="cc" width="656" height="391" class="alignnone size-large wp-image-1227" /></a>

日本でとても人気のあるフレームワーク、CakePHPですが話題の依存性管理ツールComposerと組み合わせる事でさらに便利に利用する事ができます。今回はその方法をVagrantを使ったデモと共にご紹介します。この記事で利用した環境のVagrantfileを使って頂くことでみなさんの手元でも同じ動作を確認できます。CakePHPをComposerからインストールした事が無い方は是非お試しください。

<h2>CakePHPをComposerで導入する利点</h2>
通常、CakePHPを利用する場合はZipかTarで配布されている最新版をダウンロードし、まるごとリポジトリに追加して開発を行うという形になります。すぐに動作させられるという点ではとても便利ですが、開発が長期になりフレームワークを最新版に差し替えたい場合に手作業が必要になります。またリポジトリ内に自分が記述したわけではないコードが大量に含まれるようになります。Composer経由でCakePHPをインストールする事で次のような利点があります。

<ul>
<li>フレームワークの最新版へのアップデートが自動化される</li>
<li>リポジトリ内にフレームワーク本体を含める必要がなく、シンプルになる</li>
<li>Composerを経由してさらに他のライブラリもインストールし運用できる</li>
</ul>

下記のアプリケーションは実際にComposerからCakePHPを導入する形で開発したアプリケーションです。CakePHPアプリケーションに通常存在する<code>lib/Cake</code>ディレクトリが存在していないのが確認できます。

<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;"><strong>ComposerでCakePHPを導入したアプリ phpfriends</strong><br>
<a href="https://github.com/yandod/phpfriends">https://github.com/yandod/phpfriends</a>
githubが落ちている時の予備
<a href="https://bitbucket.org/yandod/phpfriends" target="_blank">https://bitbucket.org/yandod/phpfriends</a>
</p>

<code>lib/Cake</code>が存在しない代わりにcomposer.json内にCakePHPをセットアップする記述があります。またTwitterのAPIを利用するアプリケーションなのでTwitter用のライブラリをセットアップする記述も含まれています。昨今のWebアプリケーションは必ず何らかのライブラリを利用しているといっても過言ではありませんがComposerを利用する事でライブラリもリポジトリに含める必要がなくなり、またバージョンアップなどの管理も自動化できます。

<h2>CakePHPをComposerで導入する手順</h2>
それでは実際にCakePHPをComposerで導入する手順を紹介します。今回の手順はVagrantfileで作成した環境で検証しました。下記のリポジトリをチェックアウトすればどなたでも記事と同じ内容の動作を確認できます。VirtualBoxとVagrantを導入の上で下記のリポジトリをクローンし、クローンしたディレクトリ内にcdします。

<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;"><strong>composer-cakephp-sample</strong><br>
<a href="https://github.com/yandod/composer-cakephp-sample">https://github.com/yandod/composer-cakephp-sample</a>
githubが落ちている時の予備
<a href="https://bitbucket.org/yandod/composer-cakephp-sample/src" target="_blank">https://bitbucket.org/yandod/composer-cakephp-sample/src</a>
</p>

リポジトリ内のVagrantfileは下記のような内容になっており、phpやcomposerをセットアップ済みのboxのダウンロードやソースコードのマウントなどが設定済です。

<pre lang="ruby">
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "candycane"
  config.vm.box_url = "https://dl.dropboxusercontent.com/s/krarg1fxw1bllk8/candycane.box"
  src_dir = './'
  doc_root = '/vagrant_data/app/webroot'
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.synced_folder src_dir, "/vagrant_data", :create => true, :owner=> 'vagrant', :group=>'www-data', :extra => 'dmode=775,fmode=775'
end
</pre>

この環境を起動して作業を行うには<code>vagrant up</code>した上で<code>vagrant ssh</code>とします。

<pre lang="cmd">
bash-3.2$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
[default] Importing base box 'candycane'...
[default] Matching MAC address for NAT networking...
[default] Setting the name of the VM...
[default] Clearing any previously set forwarded ports...
[default] Creating shared folders metadata...
[default] Clearing any previously set network interfaces...
[default] Preparing network interfaces based on configuration...
[default] Forwarding ports...
[default] -- 22 => 2222 (adapter 1)
[default] -- 80 => 8080 (adapter 1)
[default] Booting VM...
[default] Waiting for VM to boot. This can take a few minutes.
[default] VM booted and ready for use!
[default] Configuring and enabling network interfaces...
[default] Mounting shared folders...
[default] -- /vagrant
[default] -- /vagrant_data
bash-3.2$ vagrant ssh
Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-23-generic x86_64)

 * Documentation:  https://help.ubuntu.com/
Welcome to your Vagrant-built virtual machine.
Last login: Sat Jul 13 17:16:28 2013 from 10.0.2.2
vagrant@precise64:~$
</pre>

この時点では存在しているのはライセンスやREADMEなどを除くと、<code>Vagrantfile</code>と<code>composer.json</code>のみです。<code>composer.json</code>にはCakePHPをPEARチャンネルからダウンロードして<code>Vendor</code>以下にセットアップするように記述されています。内容は下記の通りです。バージョン番号が指定されている部分を変更すれば自由に公開されているバージョンから好きなバージョンのCakePHPを導入できます。

<pre lang="javascript">
{
    "name": "status-site",
    "repositories": [
        {
            "type": "pear",
            "url": "http://pear.cakephp.org"
        }
    ],
    "require": {
        "pear-cakephp/cakephp": "2.4.0-beta"
    },
    "config": {
        "vendor-dir": "Vendor/"
    }
}
</pre>

それでは実際にCakePHPのインストールを実行します。ソースコードが配置されいている<code>/vagrant_data</code>に移動してから<code>composer install</code>を実行します。

<pre lang="cmd">
vagrant@precise64:~$ cd /vagrant_data/
vagrant@precise64:/vagrant_data$ composer install
Loading composer repositories with package information
Initializing PEAR repository http://pear.cakephp.org
Installing dependencies (including require-dev)
  - Installing pear-pear.cakephp.org/cakephp (2.4.0beta)
    Downloading: 100%         
Writing lock file
Generating autoload files
vagrant@precise64:/vagrant_data$ 
</pre>

これによりVendor以下にCakePHPがダウンロードされセットアップされました。通常のCakePHPとは若干異なるパスに展開されている点がわかります。またこの時点ではライブラリだけが存在しておりアプリケーションを配置する<code>app</code>ディレクトリは存在していません。

<pre lang="cmd">
vagrant@precise64:/vagrant_data$ ls -l
total 20
-rwxrwxr-x 1 vagrant www-data  276 Jul 19 10:56 composer.json
-rwxrwxr-x 1 vagrant www-data 1291 Jul 19 11:10 composer.lock
-rwxrwxr-x 1 vagrant www-data 1078 Jul 19 10:56 LICENSE
-rwxrwxr-x 1 vagrant www-data   48 Jul 19 10:56 README.md
-rwxrwxr-x 1 vagrant www-data  459 Jul 19 10:56 Vagrantfile
drwxrwxr-x 1 vagrant www-data  204 Jul 19 11:10 Vendor
vagrant@precise64:/vagrant_data$ ls -l ./Vendor/pear-pear.cakephp.org/CakePHP/
total 0
drwxrwxr-x 1 vagrant www-data 170 Jul 19 11:09 bin
drwxrwxr-x 1 vagrant www-data 782 Jul 19 11:10 Cake
drwxrwxr-x 1 vagrant www-data 102 Jul 19 11:09 data
</pre>

次にアプリケーションを配置する<code>app</code>側の作成を行います。一見すると手作業が必要に見えますが、実はCakePHPのbake機能を使うことでアプリケーションに必要なファイルやディレクトリを生成することができます。今回、CakePHP本体がイレギュラーな場所に配置されており、こういった際はCAKE_CORE_INCLUDE_PATHの設定を修正する必要があります。しかしbakeを利用する事でこの設定修正も自動で行われ非常に便利です。作成を行うにはbakeコマンドを下記のように実行します。途中で何度か確認される項目は問題が無ければデフォルトのままで大丈夫です。

<pre lang="cmd">
vagrant@precise64:/vagrant_data$ ./Vendor/pear-pear.cakephp.org/CakePHP/bin/cake bake --app app

Welcome to CakePHP v2.4.0-beta Console
---------------------------------------------------------------
App : app
Path: /vagrant_data/app/
---------------------------------------------------------------
Warning Error: scandir(/vagrant_data/app/): failed to open dir: No such file or directory in [/vagrant_data/Vendor/pear-pear.cakephp.org/CakePHP/Cake/Console/Command/Task/ProjectTask.php, line 52]

Warning Error: scandir(): (errno 2): No such file or directory in [/vagrant_data/Vendor/pear-pear.cakephp.org/CakePHP/Cake/Console/Command/Task/ProjectTask.php, line 52]

Warning Error: array_diff(): Argument #1 is not an array in [/vagrant_data/Vendor/pear-pear.cakephp.org/CakePHP/Cake/Console/Command/Task/ProjectTask.php, line 52]

What is the path to the project you want to bake?  
[/vagrant_data/app] > 
What is the path to the directory layout you wish to copy?  
[/vagrant_data/Vendor/pear-pear.cakephp.org/CakePHP/Cake/Console/Templates/skel] > 
Skel Directory: /vagrant_data/Vendor/pear-pear.cakephp.org/CakePHP/Cake/Console/Templates/skel
Will be copied to: /vagrant_data/app
---------------------------------------------------------------
Look okay? (y/n/q) 
[y] > 
---------------------------------------------------------------
Created: app in /vagrant_data/app
---------------------------------------------------------------
 * Random hash key created for 'Security.salt'
 * Random seed created for 'Security.cipherSeed'
 * Cache prefix set
 * app/Console/cake.php path set.
CakePHP is not on your `include_path`, CAKE_CORE_INCLUDE_PATH will be hard coded.
You can fix this by adding CakePHP to your `include_path`.
 * CAKE_CORE_INCLUDE_PATH set to /vagrant_data/Vendor/pear-pear.cakephp.org/CakePHP in webroot/index.php
 * CAKE_CORE_INCLUDE_PATH set to /vagrant_data/Vendor/pear-pear.cakephp.org/CakePHP in webroot/test.php
   * Remember to check these values after moving to production server
Project baked successfully!
Your database configuration was not found. Take a moment to create one.
---------------------------------------------------------------
Database Configuration:
---------------------------------------------------------------
Name:  
[default] > ^C
</pre>

その後、database.phpの設定についても入力にしたがって自動で生成することができますが、ひとまずここで中断しています。これで無事にCakePHP本体のセットアップとアプリケーションの生成が完了しました。あとは<code>http://127.0.0.1:8080</code>にアクセスすれば下記のように初期画面が表示され、CakePHPが動作している事が確認できます。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/07/CakePHP__the_rapid_development_php_framework__Home.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/07/CakePHP__the_rapid_development_php_framework__Home-1024x642.png" alt="CakePHP__the_rapid_development_php_framework__Home" width="1024" height="642" class="alignnone size-large wp-image-1260" /></a>

あとは必要に応じて<code>composer.json</code>の内容を調整すればライブラリやフレームワークを追加、変更しながら開発を進められます。Engine Yard CloudのようなPaaSではcomposer.jsonが含まれるリポジトリをデプロイすると自動的にライブラリのインストールを行います。そのため、Vendor以下のファイルはリポジトリにはコミットせず、それぞれの環境でcomposerコマンドを通じてセットアップされるという形になる点に注意してください。

一見難しそうに見えるCakePHPとComposerの組み合わせが簡単に利用できる事がお分かり頂けたでしょうか？またVagrantfileを使ったポータブルな開発環境も体験できるかと思いますので宜しければこのデモの手順をお試し頂ければと思います。

Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。Composerを利用したアプリケーションをデプロイする際は、Engine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/trial"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>
