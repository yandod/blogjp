---
layout: post
status: publish
published: true
title: Chef + VagrantによるPHP5.3 + MySQL + nginxの開発環境
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1108
wordpress_url: http://www.engineyard.co.jp/blog/?p=1108
date: 2013-06-18 12:48:47.000000000 +09:00
categories:
- Uncategorized
tags: []
comments:
- id: 63
  author: CakeFest2013で発表されたCakePHP3の未来 | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/cakephp3-on-cakefest/
  date: '2013-09-04 22:33:24 +0900'
  date_gmt: '2013-09-04 13:33:24 +0900'
  content: '[...] &#8211; a set on Flickr CakePHPをComposerで導入する手順(Vagrantでのデモ環境同梱)
    Chef + VagrantによるPHP5.3 + MySQL + nginxの開発環境 Engine Yard Cloud上のPHPにCandyCaneをデプロイ
    CakeFest 2013 Photos #cakefest @cakephp | [...]'
- id: 83
  author: さよならXAMPP、こんにちはVagrant | おいしいCocoaの飲み方
  author_email: ''
  author_url: http://blog.objc.jp/?p=1931
  date: '2013-11-03 09:00:12 +0900'
  date_gmt: '2013-11-03 00:00:12 +0900'
  content: '[...] Chef + VagrantによるPHP5.3 + MySQL + nginxの開発環境 [...]'
- id: 98
  author: PHPの開発に使えるVagrantfileのまとめ | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/vagrantfile-for-php/
  date: '2013-12-01 16:52:22 +0900'
  date_gmt: '2013-12-01 07:52:22 +0900'
  content: '[&#8230;] Vagrantの基本について知りたい方は過去の記事をどうぞ Chef + VagrantによるPHP5.3 + MySQL
    + nginxの開発環境 | Engine Yard Blog JP [&#8230;]'
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/06/965238_323490164448578_1537338318_o.jpg"><img class="alignnone size-large wp-image-1115" alt="965238_323490164448578_1537338318_o" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/06/965238_323490164448578_1537338318_o-1024x682.jpg" width="1024" height="682" /></a>

2013/6/1に大阪、産業創造館で開催され<a href="http://conference.kphpug.jp/2013/program/" target="_blank">たPHPカンファレンス関西2013</a>にスポンサーとして参加しました。3年目を迎えた関西PHPユーザーグループによるカンファレンスは今年も大盛況のうちに幕を閉じていました。今回はEngine Yard CloudとEngine Yard Localでも利用されているChefとVagrantについて入門的な内容で講演を行いました。
<h3>ChefとVagrantを活用した開発環境</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/06/スクリーンショット_2013_06_18_12_19.png"><img class="alignnone size-full wp-image-1120" alt="スクリーンショット_2013_06_18_12_19" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/06/スクリーンショット_2013_06_18_12_19.png" width="692" height="328" /></a>
今回、Chefの利用経験も無い方向けにVagrantについてお話しましたが、多くの方から「<strong>便利そう」「すぐに使いたい」</strong>という感想をいただきました。VagrantはVirtualBoxにインストールしたLinuxにさまざまな設定を行なってFTPやSCPなどをしないですぐに開発が出来る所までを自動で設定します。いわば<strong>最も面倒な方法で作る最高の開発環境をコマンド一発で構築するツール</strong>です。
これまでなら手軽さを得る為に本番環境に近づける事を諦めるケースが多かったとおもいますが、Chefなどを通じて限りなく本番環境に近い環境を手元に作る事ができます。

PHP開発者の方がすぐに使えるサンプルのVagrantfileをこちらで公開していますので、まずはこちらを試してみてください。(スターして頂けると助かります。)
<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;"><strong>PHP5.3 + MySQL5.5 + Nginx の環境を作成するVagrantfileとレシピ</strong>
<a href="https://github.com/yandod/php5-nginx-vagrant-sample" target="_blank">https://github.com/yandod/php5-nginx-vagrant-sample</a></p>
なお、今回はミニマムでわかりやすい構成にする為にコミュニティで公開されているクックブックは一切使わずにシンプルなレシピを同梱しています。レシピの書き方についても順次改善していくつもりです。カンファレンスで公開した際にはPHPUnitのインストールは含めていませんでしたが、同梱しておくと便利かとおもい追加しています。

<a href="https://github.com/yandod/php5-nginx-vagrant-sample/blob/master/cookbooks/candycane_cookbook/recipes/default.rb" target="_blank">cookbooks/candycane_cookbook/recipes/default.rb</a>
<pre lang="ruby" escaped="true">execute "apt-get" do
  command "apt-get update"
end

%w{nginx php5 php5-mysql php5-cli php5-fpm php-pear mysql-server}.each do |pkg|
  package pkg do
    action [:install, :upgrade]
  end
end

execute "phpunit-install" do
  command "pear config-set auto_discover 1; pear install pear.phpunit.de/PHPUnit"
  not_if { ::File.exists?("/usr/bin/phpunit")}
end

log node[:doc_root]
template "/etc/nginx/conf.d/php-fpm.conf" do
  mode 0644
  source "php-fpm.conf.erb"
end

%w{mysql php5-fpm nginx}.each do |service_name|
    service service_name do
      action [:start, :restart]
    end
end</pre>
この環境は主にCakePHPやLaravelを動かすのに使っていますが他の用途にも利用できるでしょう。このクックブックについてはCakePHPのコアデベロッパーのMark Storyさんからもイイねと言って頂けました。
<blockquote class="twitter-tweet"><a href="https://twitter.com/yando">@yando</a> Looks great :D

— Mark Story (@mark_story) <a href="https://twitter.com/mark_story/statuses/344641151132897281">June 12, 2013</a></blockquote>
&nbsp;
<h3>Engine Yard CloudとEngine Yard Local</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/06/スクリーンショット_2013_06_18_12_19-2.png"><img class="alignnone size-full wp-image-1125" alt="スクリーンショット_2013_06_18_12_19 2" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/06/スクリーンショット_2013_06_18_12_19-2.png" width="621" height="383" /></a>
現在はRubyのみの対応となっていますがEngine Yardが提供する<a href="http://www.engineyard.co.jp/products/cloud" target="_blank">Engine Yard Cloud</a>と<a href="http://www.engineyard.co.jp/products/local" target="_blank">Engine Yard Local</a>はクラウドとVagrantとChefを構築済み、かつカスタマイズ可能な形で提供しています。独自にChefのレシピや監視ツールやデプロイツールの作りこみを行なっていくとすこしづつEngine Yard的なものを作っていく事になりますが、その完成品を提供しているという形です。オープンソースの組み合わせで実装されている事もあり内部へのアクセスやカスタマイズも自由に出来る点も個人的に気に入っています。

Chefなどのプロビジョニングツールの広まりとVagrantの開発者への普及は今後も加速していく中で、同じ組み合わせのサービスとプラクティスが製品になっているというのはなかなかおもしろいのではと思っていますが、どうでしょうか？
利用やカスタマイズについてのご相談やご質問、内緒話はいつでもお声がけください。
<h3>スライドと動画</h3>
<script async class="speakerdeck-embed" data-id="7afa7840acb9013071af5a1918864baf" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

<iframe style="border: 0px none transparent;" src="http://www.ustream.tv/embed/recorded/33618825?v=3&amp;wmode=direct" height="572" width="720" frameborder="0" scrolling="no"></iframe>

<a style="padding: 2px 0px 4px; width: 400px; background: #ffffff; display: block; color: #000000; font-weight: normal; font-size: 10px; text-decoration: underline; text-align: center;" href="http://www.ustream.tv/" target="_blank">Video streaming by Ustream</a>
