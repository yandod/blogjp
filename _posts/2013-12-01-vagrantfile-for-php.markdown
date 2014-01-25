---
layout: post
status: publish
published: true
title: PHPの開発に使えるVagrantfileのまとめ
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 2003
wordpress_url: http://www.engineyard.co.jp/blog/?p=2003
date: 2013-12-01 01:23:24.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/名称未設定-21.png" alt="名称未設定-2" width="951" height="501" class="alignnone size-full wp-image-2005" />

このエントリは<a href="http://qiita.com/advent-calendar/2013/php">PHP Advent Calendar 2013 - Qiita [キータ]</a>の1日目です。

PHPの開発に幅広く利用されるようになったVagrantですが、公開されているVagrantfileが<strong>GitHub上だけでも300件以上と色々とある</strong>のでまとめておこうと思います。

<div class="note">
GitHubでの検索結果
<a href="https://github.com/search?o=desc&q=Vagrant+php&ref=searchresults&s=stars&type=Repositories" target="_blank">Search · Vagrant php</a>

Vagrantの基本について知りたい方は過去の記事をどうぞ
<a href="http://www.engineyard.co.jp/blog/2013/chef-and-vagrant-gives-you-next-dev/">Chef + VagrantによるPHP5.3 + MySQL + nginxの開発環境 | Engine Yard Blog JP</a>
</div>

<h3><a href="https://github.com/yandod/php5-nginx-vagrant-sample" target="_blank">yandod/php5-nginx-vagrant-sample</a></h3>
こちらは手前味噌ですが、自分が使っているVagrantfileです。素のPHPやPHPUnit、各種フレームワークの動作検証に使うためにPHP5.5とNginxを構築しています。
またデータベースとしてMySQLとPostgreSQLを両方セットアップしてあり、ImageMagickも入っているあたりも特徴かと思います。
クックブックは当初は同梱していましたが、再利用性を高める為に「<a href="https://github.com/yandod/omusubi" target="_blank">omusubi</a>」クックブックとして分離し、Berkshelfを使って導入する形に改善しました。

<h3><a href="https://github.com/10up/varying-vagrant-vagrants" target="_blank">10up/varying-vagrant-vagrants</a></h3>
通称、「VVV」と呼ばれるVagrantfileでWordPressのコア開発をするために作られています。実際にコア開発者がコントリビュートしているという事で半公式のVagrantfileです。
PHPは5.4.20、nginx1.4.3になっています。

<h3><a href="https://github.com/dirkaholic/vagrant-php-dev-box" target="_blank">dirkaholic/vagrant-php-dev-box</a></h3>
 Nginx, php-fpm, MongoDBの組み合わせをベースにしたVagrantfile。プロビジョニングにはPuppetが使われています。他にもNode.jsやless、MySQL、Capistranoなどがインストールされています。

<h3>r8/vagrant-lamp</h3>
各種CMSなどとセットでLAMP環境が作られています。メールのデバッグを行うMailCatcherが導入されているのが特徴的です。Apacheのvhostsベースの運用を想定しています。
<pre>
Apache
MySQL
php
phpMyAdmin
Xdebug with Webgrind
zsh with oh-my-zsh
git, subversion
mc, vim, screen, tmux, curl
MailCatcher
Composer
Phing
Drupal utils:
Drush
Wordpress utils:
WP-Cli
wp2github.py
Magento utils:
n98-magerun
modman
modgit
Node.js with following packages:
CoffeeScript
Grunt
Bower
Yeoman
LESS
CSS Lint
</pre>

<h3><a href="https://github.com/bryannielsen/Laravel4-Vagrant" target="_blank">bryannielsen/Laravel4-Vagrant</a></h3>
その名の通りLaravel4を使った開発の為のVagrantfile。Apacheベースになっています。

<pre>
OS - Ubuntu 12.04
Apache - 2.4.6
PHP - 5.5.4
MySQL - 5.5.32
PostgreSQL - 9.1
Beanstalkd - 1.4.6
Redis - 2.2.12
Memcached - 1.4.13
</pre>

<h3><a href="https://github.com/MiniCodeMonkey/Vagrant-LAMP-Stack" target="_blank">MiniCodeMonkey/Vagrant-LAMP-Stack</a></h3>
こちらもその名の通りLAMPスタックを作るVagrantfile。postfixが入っている点が特徴的なのと簡易的な情報表示を実装しています。

<pre>
Apache 2
MySQL
PHP 5.4 (with mysql, curl, mcrypt, memcached, gd)
memcached
postfix
vim, git, screen, curl, composer
</pre>

<h3><a href="https://github.com/shin1x1/vagrant-phpenv-phpbuild" target="_blank">shin1x1/vagrant-phpenv-phpbuild</a></h3>
shin1x1さん作のVagrantfile。3系統のPHPをポート番号で分けて利用できるようになっています。ベースになるOSがCentOSになっている点も特徴です。

<h3><a href="https://github.com/ramsey/vagrant-php-src-dev" target="_blank">ramsey/vagrant-php-src-dev</a></h3>
こちらはPHPのコアコミュニティのBen Ramsey氏のVagrantfileでPHPコアの開発をする事を目的に作られています。またCakePHPやLithiumで活動していたJoel Perras氏のコードも入っています。

<strong>追記</strong>
<h3><a href="http://share.ez.no/blogs/bruce-morrison/ez-publish-5-virtual-machine" target="_blank">brucem/vagrant-puppet-ezpublish</a></h3>
CMSのeZ Publishがすぐに使えるVagrantfileです。Puppetを使ってプロビジョニングを行い、UbuntuかAWSを使うようになっています。

<hr>
Vagrantfileはプロジェクト毎に作成する性格のものですので、各自自分のプロジェクトに合ったものを作るなり利用する事になりますが、それにしてもよくもまぁ乱立したものですね。細かいカスタマイズはするにせよ、かなり参考になるものがあるのではと思います。

2日目は@msngさんです。お楽しみに！

<strong>[PR] Engine YardのPaaSを利用すればChefを使った運用の強力にサポート。クックブックのコンサルティングも提供しています。</strong>
<div><a href="http://ey.io/noyakshave"><img class="alignnone size-full wp-image-1889" style="border: 1px solid black;" alt="noyakshave_seminar_small" src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png" /></a></div>
