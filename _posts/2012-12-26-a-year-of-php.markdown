---
layout: post
status: publish
published: true
title: 2012年のPHP周辺の話題振り返り
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 423
wordpress_url: http://www.engineyard.co.jp/blog/?p=423
date: 2012-12-26 11:28:20.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/php-logo.jpeg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/php-logo-300x210.jpeg" alt="" title="php-logo" width="300" height="210" class="alignnone size-medium wp-image-424" /></a>

2012年もとうとう終わりますね。スッキリとした気持ちで2013年を迎える為に、この1年のPHPに関する出来事をまとめてみることにします。なお今回の記事の内容は<a href="https://www.facebook.com/shimokitazawa.osscafe" target="_blank">下北沢オープンソースカフェ</a>で隔週火曜日に開催しているShimokita.phpの生放送で話した内容から抜粋している形です。ゆるいフンイキではありますが動画でご覧になる方は下記をどうぞ。

http://www.youtube.com/watch?v=iGQCILzVKlw


<h2>PHP本体について</h2>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/プログラミング言語_PHPの歴史_-_pastport.png" alt="プログラミング言語_PHPの歴史_-_pastport" width="638" height="410" class="alignnone size-full wp-image-2022" />
2012年はPHP本体の開発は非常に活発でした。ほぼ毎月リリースが行われており、<strong>PHP5.3は5.3.10から5.3.20まで、PHP5.4は5.4.0から5.4.10まで</strong>バージョンが進んでいます。(<a href="http://pastport.jp/user/yandod/timeline/php-history" target="_blank">年表にまとめたページはこちら</a>)この中には重要なセキュリティの修正も含まれておりPHPを利用中のユーザは最新のPHPが推奨されています。また<span style="color:red"><strong>PHP5.3については以降は重要なセキュリティ修正しか行われない終了フェーズに入ります。新規に構築する環境ではPHP5.4を導入する事を前提</strong></span>に考えていく必要があります。PHP5.3以降にはさまざまな新機能が追加されていますのでその概要についても合わせて知っておきましょう。
実態としてはPHP5.3の新機能を業務に取り入れて開発している人が半分いるかどうかといった所な気がします。

PHP5.3
<ul>
	<li>名前空間</li>
	<li>無名関数</li>
	<li>静的遅延束縛</li>
</ul>

PHP5.4
<ul>
	<li>トレイト</li>
	<li>Array short syntax</li>
	<li>組み込みのウェブサーバー</li>
</ul>

PHP5.5
<ul>
	<li>ジェネレーター</li>
	<li>finally</li>
</ul>

<h2>カンファレンス・勉強会</h2>
日本の各地で勉強会やカンファレンスが行われました。どのイベントも多くの参加者が集まり、内容も充実していたようです。これまであまりイベントに参加しなかった方も来年は機会を見つけて参加してみると多くの気づきがあるのではないでしょうか。

カンファレンス
<a href="http://phpcon.php.gr.jp/hokkaido/2012/">PHPカンファレンス北海道</a>
<a href="http://conference.kphpug.jp/2012/">PHPカンファレンス関西2012</a>
<a href="http://phpcon.php.gr.jp/w/2012/">PHPカンファレンス2012 | 日本最大のPHPの祭典</a>
<a href="http://www.phpmatsuri.net/2012/">PHP Matsuri 2012</a>

勉強会
<a href="https://www.facebook.com/pstudy.tokyo?fref=ts">PHP勉強会@東京</a>
<a href="https://www.facebook.com/groups/436413099733710/?fref=ts">Kansai PHP Users Group</a>
<a href="http://www.local.or.jp/clubs/php">PHP部 | LOCAL</a>
<a href="https://www.facebook.com/fukuoka.p?fref=ts">Fukuoka.php</a>

<h2>ネット上の話題</h2>
今年もさまざまなPHPに関する話題がネット上を賑わせました。気がついた範囲でピックアップしてみると<strong>「最新の技術・正しい方法」や「きれいなコード・ひどいコード」といった話題</strong>が多く、<span style="color:red"><strong>多くの人が正しいPHPの開発手法を学びたい</strong></span>という意欲を持っているように見えます。またセキュリティに関する話題も感心が高く、公開されると必ず話題のエントリになっているようです。見逃しているものもあるでしょうし、読み返してみると面白いかもしれません。またHerokuやAmazon EC2などクラウドに関する記事も昨年に比べると増加してきているように見えます。

<table>
<tr>
<th>タイトル</th>
<th>ブクマ数</th>
<tr>
<td>
<a href="http://d.hatena.ne.jp/inouetakuya/20120105/1325766281">Emacs 厨だけど、PHP IDE「PhpStorm」だけはベツバラな理由 - 彼女からは、おいちゃんと呼ばれています</a>
</td>
<td>116</td>
</tr>
<tr>
<td>
<a href="http://d.hatena.ne.jp/hnw/20120115">WebスクレイピングライブラリGoutteで遊んでみる - hnwの日記</a>
</td>
<td>465</td>
</tr>
<tr>
<td>
<a href="http://d.hatena.ne.jp/serihiro/20111226/1324905489">職業プログラマになって考えた「良いコード」とは？ - seri::Programing Diary</a>
</td>
<td>445</td>
</tr>
<tr>
<td>
<a href="http://d.hatena.ne.jp/Hamachiya2/20120215/php_security">5分でできるPHPセキュリティ対策 - ぼくはまちちゃん！(Hatena)</a>
<td>1461</td>
</tr>
<tr>
<td>
<a href="http://www.slideshare.net/taketyan/phpunit-11922674">PHPUnit でテスト駆動開発を始めよう</a>
</td>
<td>265</td>
</tr>
<tr>
<td>
<a href="http://c-brains.jp/blog/wsg/12/03/13-135316.php">最近 PHP のセットアップ時にいつもやってる設定 | バシャログ。</a>
</td>
<td>400</td>
</tr>
<tr>
<td>
<a href="http://suzuzuzuru.blogspot.jp/2012/03/php60.html">味のりとこんにゃくゼリーのエンジニアブログ: phpを高速化する60の方法</a>
</td>
<td>291</td>
</tr>
<tr>
<td>
<a href="http://code-life.net/?p=1900">CakePHP初学者が知るべき６つのこと | Code Life</a>
</td>
<td>120</td>
</tr>
<tr>
<td>
<a href="http://www.slideshare.net/yandod/php-class">PHP classの教室</a>
</td>
<td>514</td>
</tr>
<tr>
<td>
<a href="http://www.publickey1.jp/blog/12/amazonphppaasgit.html">Amazonクラウド、PHP対応PaaS機能を追加。Gitによるデプロイも可能に － Publickey</a>
</td>
<td>110</td>
</tr>
<tr>
<td>
<a href="http://ulog.cc/a/higan96/14248">やってみた「WebデザイナーやノンプログラマーにおすすめしたいPHPの勉強法」 - @higan96の本館</a>
</td>
<td>674</td>
</tr>
<tr>
<td>
<a href="http://www.slideshare.net/taketyan/php-mysql-mapreduce">PHP と MySQL でカジュアルに MapReduce する</a>
</td>
<td>107</td>
</tr>
<tr>
<td>
<a href="http://d.hatena.ne.jp/ku-suke/20120404">開発中のiPhoneアプリを自前サーバで配布する方法 - ku-sukeのはてなダイアリー</a>
</td>
<td>697</td>
</tr>
<tr>
<td>
<a href="http://kachibito.net/web-service/unclassroom.html">穴埋め問題を解くような形式でPHPを学べる勉強サイト・(un)classroom - かちびと.net</a>
</td>
<td>531</td>
</tr>
<tr>
<td>
<a href="http://www.infiniteloop.co.jp/blog/2012/04/lord-of-knights-php-mysql/">「Lord of Knights の裏側見せます！～Unity + PHP + MySQL で作るスマートフォンゲーム開発～」の資料を公開しました | 株式会社インフィニットループ技術ブログ</a>
</td>
<td>592</td>
</tr>
<tr>
<td>
<a href="http://blog.candycane.jp/archives/1375">HerokuでPHPをmbstring付きで動かす&amp;パフォーマンス比較 : candycane development blog</a>
</td>
<td>108</td>
</tr>
<tr>
<td>
<a href="http://qiita.com/items/26162a4ebcbbb351b879">PHPerがMacbookAirを買ったら直ぐにすること 2012 #PHP #Mac #Apache #MySQL #homebrew - Qiita</a>
</td>
<td>592</td>
</tr>
<tr>
<td>
<a href="http://engineering.crocos.jp/post/21478792903/crocos">Crocos を支える技術 :: Crocos Engineering Blog</a>
</td>
<td>128</td>
</tr>
<tr>
<td>
<a href="http://www.slideshare.net/ockeghem/phpcondo">徳丸本に載っていないWebアプリケーションセキュリティ</a>
</td>
<td>634</td>
</tr>
<tr>
<td>
<a href="http://gihyo.jp/dev/serial/01/phpasm/0001">第1回　PHPでアセンブラを作ってみた：PHPプログラムで学ぶアセンブラのしくみ｜gihyo.jp … 技術評論社</a>
</td>
<td>107</td>
</tr>
<tr>
<td>
<a href="http://blog.tokumaru.org/2012/05/php-cgi-remote-scripting-cve-2012-1823.html">CGI版PHPにリモートからスクリプト実行を許す脆弱性(CVE-2012-1823) | 徳丸浩の日記</a>
</td>
<td>154</td>
</tr>
<tr>
<td>
<a href="http://d.hatena.ne.jp/cakephper/20120507/1336353452">facebookにPHP CGIの脆弱性を試してみたら面白い対策がされていた！！ - cakephperの日記(CakePHP, MongoDB)</a>
</td>
<td>408</td>
</tr>
<tr>
<td>
<a href="http://www.slideshare.net/yandod/40-php-class">40分濃縮 PHP classの教室</a>
</td>
<td>573</td>
</tr>
<tr>
<td>
<a href="http://www.moongift.jp/2012/05/20120530-3/">PHPでもリアルタイムWeb。node.php「React」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a>
</td>
<td>122</td>
</tr>
<tr>
<td>
<a href="http://www.moongift.jp/2012/06/20120603/">多彩なフレームワークに対応したPHP向け認証ライブラリ「Opauth」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a>
</td>
<td>319</td>
</tr>
<tr>
<td>
<a href="http://d.hatena.ne.jp/koyhoge/20120605/animita">「あにみた!」ができるまで - Blog::koyhoge</a>
</td>
<td>112</td>
</tr>
<tr>
<td>
<a href="http://tech.a-listers.jp/2012/06/14/exploring-expressions-emotions-github-commit-messages/">喜びの多いプログラミング言語はObjective-CとPHPと判明 « A-Listers</a>
</td>
<td>405</td>
</tr>
<tr>
<td>
<a href="http://d.hatena.ne.jp/Kenji_s/20120628/fuelphp1st">FuelPHP 入門書の決定版『はじめてのフレームワークとしての FuelPHP』が発売されます - A Day in Serenity @ kenjis</a>
</td>
<td>116</td>
</tr>
<tr>
<td>
<a href="http://takahashifumiki.com/web/programing/2209/">PHPはバグレポートがバグッてる。だがそれがいい。 | 高橋文樹.com</a>
</td>
<td>122</td>
</tr>
<tr>
<td>
<a href="http://blog.candycane.jp/archives/1534">「8時間耐久 PHP構築の教室」を開催しました。 : candycane development blog</a>
</td>
<td>225</td>
</tr>
<tr>
<td>
<a href="http://ja.phptherightway.com/">PHP: The Right Way</a>
</td>
<td>482</td>
</tr>
<tr>
<td>
<a href="http://phpjs.hertzen.com/">php.js - PHP VM with JavaScript</a>
</td>
<td>148</td>
</tr>
<tr>
<td>
<a href="http://www.1x1.jp/blog/2012/08/ecent_php_news_201208.html">6分でわかる最近のPHP ― 2012夏 - Shin x blog</a>
</td>
<td>793</td>
</tr>
<tr>
<td>
<a href="http://d.hatena.ne.jp/sotarok/20120914/nequal_and_crocos">僕と nequal と Crocos - 肉とご飯と甘いもの @ sotarok</a>
</td>
<td>177</td>
</tr>
<tr>
<td>
<a href="http://www.slideshare.net/ockeghem/phpconf2012">徳丸本に学ぶ 安全なPHPアプリ開発の鉄則2012</a>
</td>
<td>369</td>
</tr>
<tr>
<td>
<a href="http://www.slideshare.net/kwatch/php55">PHP5.5新機能「ジェネレータ」初心者入門</a>
</td>
<td>363</td>
</tr>
<tr>
<td>
<a href="http://docs.komagata.org/4973">レガシーPHPプロジェクトあるある - komagata</a>
</td>
<td>186</td>
</tr>
<tr>
<td>
<a href="http://www.slideshare.net/VOYAGE_GROUP/php-14368949">Phpではじめるオブジェクト指向(公開用)</a>
</td>
<td>261</td>
</tr>
<tr>
<td>
<a href="http://www.slideshare.net/MugeSo/mvc-14469802">やはりお前らのMVCは間違っている</a>
</td>
<td>589</td>
</tr>
<tr>
<td>
<a href="http://www.slideshare.net/yandod/psrphp">新標準PSRに学ぶきれいなPHP</a>
</td>
<td>220</td>
</tr>
<tr>
<td>
<a href="http://www.1x1.jp/blog/2012/09/book_cakephp2.html">いまどきの技術本執筆環境 – 「CakePHP2実践入門」 - Shin x blog</a>
</td>
<td>194</td>
</tr>
<tr>
<td>
<a href="http://www.msng.info/archives/2012/10/facebook-login-with-php.php">PHP で「Login with Facebook」を実装する基本的な方法まとめ - 頭ん中</a>
</td>
<td>194</td>
</tr>
<tr>
<td>
<a href="http://php6.jp/linux/2012/10/13/memcached_session_php_amazon_ec2/">MemcachedでPHPのセッション管理 on AmazonEC2 « Linux練習帳</a>
</td>
<td>125</td>
</tr>
<tr>
<td>
<a href="http://ac7.tumblr.com/post/33569124174">nakano_neko, 画像の右側が外注さんに頼んだソースコード。左側が僕が書きなおしたソースコード。...</a>
</td>
<td>377</td>
</tr>
<tr>
<td>
<a href="http://d.hatena.ne.jp/Kenji_s/20121016/why_fuelphp_boom">何故 FuelPHP は流行っているのか？ - A Day in Serenity @ kenjis</a>
</td>
<td>192</td>
</tr>
<tr>
<td>
<a href="http://blog.56doc.net/web%E6%8A%80%E8%A1%93/%E6%96%B0%E3%82%AF%E3%83%A9%E3%82%A6%E3%83%89%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9%E3%80%8Cphp%20apps%E3%80%8D%E3%81%8C%E6%9C%80%E5%BC%B7%E3%81%AE%E7%84%A1%E6%96%99%E3%83%96%E3%83%AD%E3%82%B0%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9%E3%81%AB%E3%81%AA%E3%82%8A%E3%81%9D%E3%81%86%E3%81%AA%E4%BB%B6%20">新クラウドサービス「PHP APPS」が最強の無料ブログサービスになりそうな件 | 56docブログ</a>
</td>
<td>630</td>
</tr>
<tr>
<td>
<a href="https://speakerdeck.com/ryuzee/cakephp-plus-jenkinsniyoruaziyairukai-fa-number-phpmatsuri">CakePHP+Jenkinsによるアジャイル開発 #phpmatsuri // Speaker Deck</a>
</td>
<td>293</td>
</tr>
<tr>
<td>
<a href="http://blog.tokumaru.org/2012/11/php548-is-vulnerable-to-hashdos.html">セキュリティ情報:PHP5.4.8、PHP5.3.18以前にhashdos脆弱性 | 徳丸浩の日記</a>
</td>
<td>109</td>
</tr>
<tr>
<td>
<a href="http://kaz29.hatenablog.com/entry/2012/11/30/173424">今時なCakePHPでの開発環境！？ - kaz29</a>
</td>
<td>322</td>
</tr>
<tr>
<td>
<a href="http://www.1x1.jp/blog/2012/12/why_use_php.html">PHPを使う理由 - Shin x blog</a>
</td>
<td>314</td>
</tr>
<tr>
<td>
<a href="http://tumblr.tokumaru.org/post/37536025211/sql">書式文字列によるSQLインジェクション攻撃例 - 徳丸浩のtumblr</a>
</td>
<td>201</td>
</tr>
<tr>
<td>
<a href="http://d.hatena.ne.jp/MugeSo/20121224/1356345261">PHPerのMVCの一体どこが間違っていたのか - MugeSoの日記</a>
</td>
<td>331</td>
</tr>
</table>

全ての話題を知っていたのなら、かなりPHPの情報を追えている方ですね。年末年始に読み返してみると来年の展望が持てるかもしれません。
