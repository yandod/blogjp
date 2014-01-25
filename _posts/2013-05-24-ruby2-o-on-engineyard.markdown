---
layout: post
status: publish
published: true
title: Ruby 2.0 がEngine Yard Cloudで利用できます
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1077
wordpress_url: http://www.engineyard.co.jp/blog/?p=1077
date: 2013-05-24 11:42:23.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/Engine_Yard_Cloud_—_Features.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/Engine_Yard_Cloud_—_Features.png" alt="Engine_Yard_Cloud_—_Features" width="854" height="613" class="alignnone size-full wp-image-1078" /></a>

これまでもご要望を頂いていたRuby2.0がEngine Yard Cloudでご利用頂けるようになりました。まずは早期アクセスとしてのリリースになりますが、皆様からのフィードバックを元に今後は標準でご利用頂けるようになります。利用の手順については別途ドキュメントがありますが、概要としては下記のような形になっております。

<ul>
	<li>Ruby 2.0の早期アクセスを有効にする</li>
	<li>Stack Selectの早期アクセスを有効にする</li>
	<li>Gentoo 2012の早期アクセスを有効にする</li>
	<li>プレリリース版のengineyard gemを使いデプロイを行う</li>
</ul>

ドキュメントはこちら<br/>
<a href="https://support.cloud.engineyard.com/entries/23880458">Engine Yard Cloud で Ruby 2.0 を始める (Use Ruby 2.0 on Engine Yard Cloud) : Engine Yard Developer Center</a>

標準の状態ですとEngine Yard Cloudはスタックを自動的に選択しますが、スタック選択機能を利用して最新のOSやツールを利用する形になります。パートナーの永和システムマネジメント様を始め、多くのRubyistの方々にご利用頂いてフィードバックを頂ければと思っております。

<h2>Rubyイベントラッシュ</h2>

ご存知の方も多いと思いますが、ここからEngine YardはRubyイベントのラッシュです。

<h3><a href="https://www.facebook.com/events/134317143424820/">Ebisu.rb #6</a></h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/8FDlrQxrEX2zqVBwNli8nWiY8exDVOZ1N-85KjlZMf0.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/8FDlrQxrEX2zqVBwNli8nWiY8exDVOZ1N-85KjlZMf0-300x300.png" alt="8FDlrQxrEX2zqVBwNli8nWiY8exDVOZ1N-85KjlZMf0" width="300" height="300" class="alignnone size-medium wp-image-1081" /></a>
こちらは毎月開催しているEbisu近辺のRubyistが集まるMeetupです。ほどほどの人数でしっぽりとやっていますが最近出来たロゴがとてもかわいいのが自慢ですね。

<h3><a href="http://rubykaigi.org/2013">RubyKaigi 2013, May 30 - Jun 1</a></h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/RubyKaigi_2013__May_30_-_Jun_1-1024x528.png" alt="RubyKaigi_2013__May_30_-_Jun_1" width="1024" height="528" class="alignnone size-large wp-image-1084" />
言わずと知れたThe RubyKaigiです。今回Engine YardからはChrisとJacobが登壇しています。また会場には僕らも居ますのでステッカーなどが欲しい方はお気軽にお声がけ頂ければと思います。

<h3><a href="http://sikachu.doorkeeper.jp/events/4108" target="_blank">sikachu meetup</a></h3>
<a href="http://sikachu.doorkeeper.jp/events/4108"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/4108_normal_1369473725_シカチュー2.png" alt="4108_normal_1369473725_シカチュー2" width="870" height="435" class="alignnone size-full wp-image-1098" /></a>
こちらは詳細調整中ですが、フィヨルドの町田さん駒形さんからお声がけ頂いたので会場提供させて頂きます。

<h3><a href="http://rubyhiroba.org/2013/">RubyHiroba 2013</a></h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/RubyHiroba_2013-1024x503.png" alt="RubyHiroba_2013" width="1024" height="503" class="alignnone size-large wp-image-1088" />
こちらはRubyKaigiの翌日のイベントです。参加無料で基本的にはLTも誰でもできるRubyの好きな人が集まる広場です。Engine Yardはブースを構えてみなさんに軽食やノベリティをお配りします。ブースやLTはまだ申し込めますので多くの人に広めたい内容がある方は是非どうぞ。

<h3><a href="http://kakutani.doorkeeper.jp/events/4073">DCI meetup w/ @saturnflyer for Rubyists #dcimeetup - kakutani</a></h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/4073_normal_1369246308_cr-header.png" alt="4073_normal_1369246308_cr-header" width="870" height="259" class="alignnone size-full wp-image-1100" />
こちらはRubyHirobaの翌日のイベントです。来日したJim Gayさんを囲んでのイベントになります。まだまだ参加受付中です。

<blockquote>
Jim Gayの旅費を支援するために開催するmeetupです。チケットが2種類あるのは、普通に参加したい方向けと、Jim Gayの旅費をより厚く支援したい方向けです。どちらのチケットを購入してもクーポンコードはお伝えします(当人の1回限りの利用でお願いします。無茶するとクーポンを失効にされてしまうと思います)
</blockquote>

まだ到着していませんが新しいステッカーやノベリティなどを用意して持ちあるくようにしますのでご興味がある方はぜひお声がけください。

<div style="border:1px solid black"><a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/728x90-banner-rails.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/05/728x90-banner-rails.png" alt="728x90-banner-rails" width="728" height="90" class="alignnone size-large wp-image-1094" /></a></div>
