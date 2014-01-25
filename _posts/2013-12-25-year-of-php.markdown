---
layout: post
status: publish
published: true
title: 2013年PHPの話題を一挙に振り返るまとめ
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 2152
wordpress_url: http://www.engineyard.co.jp/blog/?p=2152
date: 2013-12-25 15:00:26.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/php-logo.jpeg" alt="php-logo" width="578" height="406" class="alignnone size-full wp-image-424" />

2013年も本当にあとわずかになりました。
本日は今年話題になったPHPについての記事を公式のリリースやはてなブックマークから抽出してきた内容を元に今年を振り返ってみましょう。PHPにとって今年はどのような一年だったのでしょうか。

参考：
<a href="http://www.engineyard.co.jp/blog/2012/a-year-of-php/">2012年のPHP周辺の話題振り返り | Engine Yard Blog JP</a>

<h3>PHPのバージョン</h3>
2013年中にリリースされたPHPのバージョンは5.3、5.4、5.5の3系統で合計29のリリースが行われました。リリースサイクルはほぼ毎月という形でした。またPHPの公式サイトがレスポンシブ対応の新しいデザインに切り替わりました。詳細は下記の通りです。

<table>
<tr><th>Version 5.4.11</th><td>2013/1/17</td></tr>
<tr><th>Version 5.3.21</th><td>2013/1/17</td></tr>
<tr><th>Version 5.4.12</th><td>2013/2/21</td></tr>
<tr><th>Version 5.3.22</th><td>2013/2/21</td></tr>
<tr><th>Version 5.4.13</th><td>2013/3/14</td></tr>
<tr><th>Version 5.3.23</th><td>2013/3/14</td></tr>
<tr><th>Version 5.4.14</th><td>2013/4/11</td></tr>
<tr><th>Version 5.3.24</th><td>2013/4/11</td></tr>
<tr><th>Version 5.4.15</th><td>2013/5/9</td></tr>
<tr><th>Version 5.3.25</th><td>2013/5/9</td></tr>
<tr><th>Version 5.4.16</th><td>2013/6/6</td></tr>
<tr><th>Version 5.3.26</th><td>2013/6/6</td></tr>
<tr><th>Version 5.5.0</th><td>2013/6/20</td></tr>
<tr><th>Version 5.4.17</th><td>2013/7/4</td></tr>
<tr><th>Version 5.3.27</th><td>2013/7/11</td></tr>
<tr><th>Version 5.5.1</th><td>2013/7/18</td></tr>
<tr><th>Version 5.5.2</th><td>2013/8/15</td></tr>
<tr><th>Version 5.4.18</th><td>2013/8/15</td></tr>
<tr><th>Version 5.5.3</th><td>2013/8/22</td></tr>
<tr><th>Version 5.4.19</th><td>2013/8/22</td></tr>
<tr><th>Version 5.5.4</th><td>2013/9/19</td></tr>
<tr><th>Version 5.4.20</th><td>2013/9/19</td></tr>
<tr><th>Version 5.5.5</th><td>2013/10/17</td></tr>
<tr><th>Version 5.4.21</th><td>2013/10/17</td></tr>
<tr><th>Version 5.5.6</th><td>2013/11/14</td></tr>
<tr><th>Version 5.4.22</th><td>2013/11/14</td></tr>
<tr><th>Version 5.5.7</th><td>2013/12/12</td></tr>
<tr><th>Version 5.4.23</th><td>2013/12/12</td></tr>
<tr><th>Version 5.3.28</th><td>2013/12/12</td></tr>
</table>

<p style="background:#99EE99;border: black dotted 1px; padding:15px">
<strong>[重要] 頻繁にバージョンアップされるPHPを最新の状態に保つにはEngine Yard Cloudの利用をお奨めします。</strong>
</p>
<h3>PHP5.5の新機能</h3>
上記のとおり、6月にPHP5.5がリリースされました。機能の追加や廃止を含むリリースでメジャーバージョンアップではありませんが、重要なリリースです。PHP5.5で追加された新機能は下記の通りです。

<ul>
<li>ジェネレータの追加</li>
<li>finally キーワードの追加</li>
<li>新しいパスワードハッシュ API</li>
<li>foreach が list() に対応</li>
<li>empty() が任意の式に対応</li>
<li>array リテラルと string リテラルのデリファレンス</li>
<li>::class によるクラス名の解決</li>
<li>OPcache 拡張モジュールの追加</li>
<li>foreach が非スカラーのキーに対応</li>
<li>Apache 2.4 ハンドラが Windows に対応</li>
<li>GD の改良</li>
</ul>

その他、廃止される機能などの詳細は<a href="http://www.php.net/manual/ja/migration55.php" target="_blank">PHPの公式ドキュメント</a>をご覧ください。

<h3>ブログ記事の総評</h3>
今年話題になったPHPに関する記事から厳選した記事が下記の20個の記事です。見逃した記事があればぜひともチェックしてみてください。

<ul>
<li><a href="https://gist.github.com/masakielastic/5457174" target="_blank">すぐれた PHP ライブラリとリソース</a></li>
<li><a href="http://www.slideshare.net/shin1x1/xampp-mamp-vagrant-php" target="_blank">Vagrant で作る PHP 開発環境</a></li>
<li><a href="http://www.slideshare.net/ockeghem/phpconf2013" target="_blank">安全なPHPアプリケーションの作り方2013</a></li>
<li><a href="http://qiita.com/mpyw/items/b00b72c5c95aac573b71" target="_blank">PHPでデータベースに接続するときのまとめ - Qiita [キータ]</a></li>
<li><a href="http://www.slideshare.net/yoku0825/devsdba" target="_blank">Devsの常識、DBAは非常識</a></li>
<li><a href="http://dqn.sakusakutto.jp/2013/11/php51to54.html" target="_blank">ソースコード20万行の大規模サイトのPHPを5.1から5.4に上げるためにやったことまとめ - DQNEO起業日記</a></li>
<li><a href="http://tech.a-listers.jp/2013/05/06/web-framework-benchmark/" target="_blank">16の言語と57のフレームワークを比較したベンチマークが凄い | A-Listers</a></li>
<li><a href="http://www.slideshare.net/techblogyahoo/phpcon2013-performance" target="_blank">本当に怖いパフォーマンスが悪い実装 #phpcon2013</a></li>
<li><a href="http://www.slideshare.net/ockeghem/xssreintroduction" target="_blank">XSS再入門</a></li>
<li><a href="https://speakerdeck.com/yandod/modanphptiyutoriaru-llmaturiban" target="_blank">モダンPHPチュートリアル (LLまつり版) // Speaker Deck</a></li>
<li><a href="http://cloverstudioceo.hatenablog.com/entry/2013/10/21/033700" target="_blank">Spikaを公開して起こった事 - ヨーロッパで働く社長のブログ</a></li>
<li><a href="http://www.msng.info/archives/2013/08/php-engineer-book.php" target="_blank">いまどきのPHP開発ノウハウを詰め込んだ『PHPエンジニア養成読本』が出るので、見所をまとめてみるよ - 頭ん中</a></li>
<li><a href="http://d.hatena.ne.jp/Kenji_s/20130221/php_regexp" target="_blank">PHP の正規表現があまりに複雑なのでまとめてみた - A Day in Serenity @ kenjis</a></li>
<li><a href="http://blog.tojiru.net/article/377526320.html" target="_blank">PHPのinterfaceとは何か - 泥のように</a></li>
<li><a href="http://www.1x1.jp/blog/2013/10/vagrant-lapp-sample.html" target="_blank">PHP開発環境のサンプルVagrantfile - Shin x blog</a></li>
<li><a href="http://kaz29.hatenablog.com/entry/2013/04/30/122642" target="_blank">「CIを半年間まわしてみて」というお題でLTをしてきました - kaz29</a></li>
<li><a href="http://www.atmarkit.co.jp/ait/articles/1308/20/news004.html" target="_blank">PHP 5.5の新機能：さっくり理解するPHP 5.5の言語仕様と「いい感じ」の使い方 (1/2) - ＠IT</a></li>
<li><a href="http://d.hatena.ne.jp/thk/20131221" target="_blank">「WEB+DB PRESS」で艦これで有名なDMMの開発体制の全貌が明らかに - 東洋黒客の凱旋</a></li>
<li><a href="http://www.engineyard.co.jp/blog/2013/vagrantfile-for-php/" target="_blank">PHPの開発に使えるVagrantfileのまとめ | Engine Yard Blog JP</a></li>
<li><a href="http://blog.sarabande.jp/post/48522241291" target="_blank">2013年において注目すべき PHP フレームワークは Laravel - Sarabande.jp</a></li>
</ul>


それぞれの月の記事と概要は下記の通りです。

<hr/>
<a href="http://ey.io/noyakshave"><img src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png"></a>
<hr/>

<h3>1月:PhpStormについてのスライドが話題に</h3>
1月の話題で特に注目すべきなのはFacebookが開発し公開しているPHPの仮想マシン、HipHopVMについての記事とPHPStormについて触れたスライドではないでしょうか。HipHopはPHPをC++に変換して実行するというコードトランスレーターをJITコンパイラへと近づけていく意欲的な試みです。この機能は最終的にはPHP本体に取り込まれるような可能性もあり今後も注目が集まりそうです。

また今年はPhpStormの利用が広がりましたが、その背景が@hisaterutanakaさんのスライドに述べられています。

<blockquote>「PHPはJavaの次に静的解析しやすい言語。これはRubyが気付いていないPHPの長所」 ―PHPメンターズと朝まで過ごしたときの言</blockquote>

PHPは言語としての弱さを指摘されることも多いですが、上記のようにコード生成や解析がしやすいという側面が先進的な取り組みの基礎になっているとも言えるでしょう。また年末年始の時間を利用したのかサイトを作ってみたという話題も（掲載できないようなサイトも含めて）話題になっていたのが特徴です。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr><tr><td><a href='http://anond.hatelabo.jp/20130104184115' target='_blank'>ド素人が完全自作SNSを作ってみてわかったこと。</a></td><td>1568</td><td>2013/01/04</td></tr>
<tr><td><a href='http://japan.cnet.com/sp/businesslife/35026228/' target='_blank'>2013年、開発者が注目すべき10のスキル - CNET Japan</a></td><td>257</td><td>2013/01/07</td></tr>
<tr><td><a href='http://phpspot.org/blog/archives/2013/01/googlefacebookt.html' target='_blank'>Google,Facebook,Twitter,Tumblr等のAPIを簡単に扱える機能豊富なPHPライブラリセット「Eden」:phpspot開発日誌</a></td><td>132</td><td>2013/01/08</td></tr>
<tr><td><a href='http://wp-d.org/2013/01/14/1938/' target='_blank'>新春座談会 このコンピュータ書がすごい！ 2013年版 | WP-D</a></td><td>347</td><td>2013/01/14</td></tr>
<tr><td><a href='http://tech.a-listers.jp/2013/01/16/speeding-up-php-based-development-with-hiphop-vm/' target='_blank'>Facebookが開発したPHPを超高速で実行する仮想マシン HipHop VM « A-Listers</a></td><td>181</td><td>2013/01/16</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/maeharin/20130118/php_ruby_love' target='_blank'>PHPを愛する試み - maeharinの日記</a></td><td>190</td><td>2013/01/18</td></tr>
<tr><td><a href='http://anond.hatelabo.jp/20130118212733' target='_blank'>ド素人が完全自作SNSを二週間運営してみてわかったこと（後始末編、技術編、モチベーション編）</a></td><td>662</td><td>2013/01/18</td></tr>
<tr><td><a href='http://blog.xao.jp/blog/cakephp/how-to-access-to-a-variaty-of-objects/' target='_blank'>CakePHPで様々なオブジェクトへのアクセスの仕方 | X->A->O</a></td><td>165</td><td>2013/01/27</td></tr>
<tr><td><a href='http://www.slideshare.net/tanakahisateru/jetbrains2-phpstorm' target='_blank'>PhpStormを使おう --高槻からは快速急行が早くなります</a></td><td>105</td><td>2013/01/30</td></tr>
</table>

<h3>2月:正規表現の話題とセキュリティ</h3>
2月はさまざまなTIPS系の話題が多く、何度か登場する正規表現の話題とセキュリティについての話題が出ています。また今年は一年を通じてエディタの話題も多かったのですが2月にVimの話題が出ています。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://photoshopvip.net/archives/45206' target='_blank'>[技術] nginxを利用した、高速サーバー構築マニュアル - Photoshop VIP</a></td><td>607</td><td>2013/02/11</td></tr>
<tr><td><a href='http://chantk-twi.pupu.jp/archives/747' target='_blank'>短期間でプログラミングを習得してWebサービスをつくるための知識と方法まとめ | らふらく ^^</a></td><td>1441</td><td>2013/02/11</td></tr>
<tr><td><a href='http://densho.hatenablog.com/entry/dendenconverter' target='_blank'>EPUBを作成するウェブサービス作ったよ - 電書ちゃんねる</a></td><td>268</td><td>2013/02/14</td></tr>
<tr><td><a href='http://blog.tokumaru.org/2013/02/purpose-and-implementation-of-the-logout-function.html' target='_blank'>ログアウト機能の目的と実現方法 | 徳丸浩の日記</a></td><td>297</td><td>2013/02/15</td></tr>
<tr><td><a href='http://liginc.co.jp/programmer/archives/4921' target='_blank'>PHPでjQueryチックにWebサイトをクローリングする方法 | 株式会社LIG</a></td><td>123</td><td>2013/02/15</td></tr>
<tr><td><a href='http://runnable.com/' target='_blank'>Edit, run, & share server-side code in your browser - Make your code Runnable</a></td><td>156</td><td>2013/02/15</td></tr>
<tr><td><a href='http://tumblr.tokumaru.org/post/43394245031/web-11' target='_blank'>勝手に査読:Webアプリにおける11の脆弱性の常識と対策 - 徳丸浩のtumblr</a></td><td>320</td><td>2013/02/18</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/do_aki/20130218/1361197742' target='_blank'>Excel は Editor ですか？ いいえ、Image Viewer です。 - do_akiの徒然想記</a></td><td>114</td><td>2013/02/19</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/murishinai/20130220/p1' target='_blank'>三項演算子である条件演算子が右結合であることの利点・妥当性と可読性について - Guinea Pig</a></td><td>171</td><td>2013/02/20</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/Kenji_s/20130221/php_regexp' target='_blank'>PHP の正規表現があまりに複雑なのでまとめてみた - A Day in Serenity @ kenjis</a></td><td>273</td><td>2013/02/21</td></tr>
<tr><td><a href='http://www.ideaxidea.com/archives/2013/02/codebird-php.html' target='_blank'>PHPからTwitter APIを叩くなら『codebird-php』が便利そう | IDEA*IDEA</a></td><td>116</td><td>2013/02/21</td></tr>
<tr><td><a href='http://blog.tokumaru.org/2013/02/security-measures-of-own-way-are-unsafe.html' target='_blank'>自己流のSQLインジェクション対策は危険 | 徳丸浩の日記</a></td><td>224</td><td>2013/02/23</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/sifue/20130224/1361713497' target='_blank'>ssh上でマウススクロールも使える大規模PHP開発向けvim+tmux環境の構築 - しふーのブログ</a></td><td>356</td><td>2013/02/24</td></tr>
<tr><td><a href='http://matome.naver.jp/odai/2136185347913005301' target='_blank'>【初心者向け】最速でphpを学ぶための厳選記事集 - NAVER まとめ</a></td><td>730</td><td>2013/02/26</td></tr>
<tr><td><a href='http://c-brains.jp/blog/wsg/13/02/27-102230.php' target='_blank'>Vim で PHP 開発するためにやってる設定 3 つほど | バシャログ。</a></td><td>108</td><td>2013/02/27</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/perlcodesample/20130227/1361928810' target='_blank'>変数に型がないということの利点について考える - サンプルコードによるPerl入門</a></td><td>405</td><td>2013/02/27</td></tr>
</table>

<h3>3月:PHPを何故使うのか</h3>
3月はPHPを何故使うのか、という意義について述べた記事が話題になっています。言語仕様の至らない点を指摘するといういつもの流れもある一方でとにかく動くサービスやプロダクトを作るべしという事を述べた体験談が見受けられます。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://ameblo.jp/nikko-inma/entry-11122429825.html' target='_blank'>PHPとかいう糞言語｜いんまのブログ</a></td><td>210</td><td>2013/03/07</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/bravewood/20130307' target='_blank'>PHPは代入と参照の違い | 2013-03-07 - bravewood の日記</a></td><td>135</td><td>2013/03/07</td></tr>
<tr><td><a href='http://blogs.itmedia.co.jp/fukuyuki/2013/03/php-57de.html' target='_blank'>カネと時間考えるならPHPやっとけ。たぶｎ ：村上福之の「ネットとケータイと俺様」：ITmedia オルタナティブ・ブログ</a></td><td>435</td><td>2013/03/08</td></tr>
<tr><td><a href='http://suzuki.tdiary.net/20130309.html#p01' target='_blank'>PHPUnit と Selenium2 を使ってブラウザベースの自動テストを実行するための最初の一歩的な何かを発表してきた - 雑文発散(2013-03-09)</a></td><td>174</td><td>2013/03/09</td></tr>
<tr><td><a href='http://blog.livedoor.jp/dankogai/archives/51858766.html' target='_blank'>404 Blog Not Found:ついに顕在化しはじめたArrayリスク</a></td><td>107</td><td>2013/03/11</td></tr>
<tr><td><a href='http://www.moongift.jp/2013/03/20130313-2/' target='_blank'>Facebook製。プログラマー向けのプロジェクト管理「Phabricator」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td><td>147</td><td>2013/03/13</td></tr>
<tr><td><a href='http://knoh.jp/answers/22cc7d73' target='_blank'>メジャーなプログラミング言語とそれらの役割を、素人でも分かるように教えてください。 - Knoh</a></td><td>1211</td><td>2013/03/13</td></tr>
<tr><td><a href='http://blog.champierre.com/973' target='_blank'>Vagrant 入門 - Windows 上に Linux の仮想マシンを簡単に用意する - 僕は発展途上技術者</a></td><td>416</td><td>2013/03/16</td></tr>
<tr><td><a href='http://www.publickey1.jp/blog/13/obama_for_america_1.html' target='_blank'>「Obama For America」の開発チームが作り上げた大規模な選挙キャンペーンシステムの舞台裏（後編） － Publickey</a></td><td>117</td><td>2013/03/18</td></tr>
<tr><td><a href='http://anond.hatelabo.jp/20130322031333' target='_blank'>プログラミング出来ない奴ちょっと来い</a></td><td>2024</td><td>2013/03/22</td></tr>
<tr><td><a href='http://www.compileonline.com/' target='_blank'>Compile and Execute Programs Online| Online IDE</a></td><td>121</td><td>2013/03/23</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/kazuhooku/20130323/1364039729' target='_blank'>なぜPHPでrequire("http://...")したらセキュリティホールなのに、Goならいいのか - kazuhoのメモ置き場</a></td><td>153</td><td>2013/03/23</td></tr>
<tr><td><a href='http://blog.verygoodtown.com/2013/03/development-user-style-guide/' target='_blank'>プログラマのための言語別コーディング規約まとめ | Web活メモ帳</a></td><td>1248</td><td>2013/03/29</td></tr>
<tr><td><a href='http://uzulla.hateblo.jp/entry/2013/03/31/223143' target='_blank'>一行でも書け、倒れるときは前のめり（または書かないで済ませる話） - uzullaがブログ</a></td><td>103</td><td>2013/04/01</td></tr>
</table>

<h3>4月:LaravelとZend OPCache</h3>
4月はLaravelとZend OPCacheについての記事が話題になっています。軽量さで人気が高まってきているLaravelとAPCに変わるキャッシュとして標準化されるOPCacheは今後は実際に利用されるケースが増えてくるでしょう。
また有用なライブラリのリストを翻訳して紹介したエントリが話題になっていました。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://www.kaasan.info/archives/2623' target='_blank'>PHPを勉強するならこれだけは言いたい！PHPのオススメ勉強法-ITかあさん</a></td><td>506</td><td>2013/04/01</td></tr>
<tr><td><a href='http://shukatsu-mirai.com/shukatsu/web-ap/' target='_blank'>初心者でも3か月でwebサービスを必ず作れるようになる！Webサービス学習資料5選 | 就活の未来 大学生のための就活支援サイト</a></td><td>815</td><td>2013/04/03</td></tr>
<tr><td><a href='http://blog.tokumaru.org/2013/04/php-displayerrors-xss.html' target='_blank'>PHPのdisplay_errorsが有効だとカジュアルにXSS脆弱性が入り込む | 徳丸浩の日記</a></td><td>115</td><td>2013/04/04</td></tr>
<tr><td><a href='http://blog.kenjiskywalker.org/blog/2013/04/04/tweets_zip_big_data/' target='_blank'>tweets.zipをMySQLに突っ込んでSQLを学ぶ(導入編) - さよならインターネット</a></td><td>275</td><td>2013/04/05</td></tr>
<tr><td><a href='http://www.moongift.jp/2013/04/20130406/' target='_blank'>意外と便利？PHP製のHTML用問い合わせ言語「htmlSQL」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td><td>159</td><td>2013/04/06</td></tr>
<tr><td><a href='http://coliss.com/articles/build-websites/operation/javascript/jquery-plugin-superbox.html' target='_blank'>[JS]lightboxの進化形、レスポンシブ対応で画像を拡大表示するスクリプト -SuperBox | コリス</a></td><td>270</td><td>2013/04/08</td></tr>
<tr><td><a href='http://wp.yat-net.com/?p=3662' target='_blank'>AWSにApache+PHP+MySQLとphpMyAdmin,vsftpdを導入する手順 - YATのBLOG</a></td><td>211</td><td>2013/04/10</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/moto_maka/20130412/1365708877' target='_blank'>iPhoneアプリにPush通知機能を実装する方法のまとめ - もとまか日記</a></td><td>130</td><td>2013/04/12</td></tr>
<tr><td><a href='http://kirinblog.com/tool/sublimetext2-emmet.html' target='_blank'>Sublime Text 2とEmmetで制作効率アップ！@福岡マークアップ勉強会 | キリンブログ</a></td><td>100</td><td>2013/04/14</td></tr>
<tr><td><a href='http://techacademy.jp/magazine/620' target='_blank'>日本語も対応！ブラウザでプログラミングが学べる「Codecademy」を実際にやってみた | TechAcademyマガジン</a></td><td>375</td><td>2013/04/16</td></tr>
<tr><td><a href='http://coliss.com/articles/web-services/online-regexp-playground.html' target='_blank'>正規表現と文字列がマッチしているか簡単にチェックできるオンラインツール -RegExp playground | コリス</a></td><td>206</td><td>2013/04/19</td></tr>
<tr><td><a href='http://blog.sarabande.jp/post/48522241291' target='_blank'>2013年において注目すべき PHP フレームワークは Laravel - Sarabande.jp</a></td><td>233</td><td>2013/04/21</td></tr>
<tr><td><a href='http://blog.1dz.jp/?eid=805' target='_blank'>Sublime Textの地味に便利なショートカット5つ | Webデザインのタネ</a></td><td>213</td><td>2013/04/22</td></tr>
<tr><td><a href='http://www.slideshare.net/t_wada/sql-antipatterns-digest' target='_blank'>SQLアンチパターン - 開発者を待ち受ける25の落とし穴 (拡大版)</a></td><td>479</td><td>2013/04/22</td></tr>
<tr><td><a href='http://blog.asial.co.jp/1152' target='_blank'>PHPからChromeにログ出力「Chrome Logger」 : アシアルブログ</a></td><td>126</td><td>2013/04/25</td></tr>
<tr><td><a href='https://gist.github.com/masakielastic/5457174' target='_blank'><strong>すぐれた PHP ライブラリとリソース</strong></a></td><td>798</td><td>2013/04/25</td></tr>
<tr><td><a href='http://www.1x1.jp/blog/2013/04/php55_replace_apc_with_zend_opcache.html' target='_blank'>PHP5.5 のコードキャッシュは APC から Zend OPcache へ - Shin x blog</a></td><td>188</td><td>2013/04/29</td></tr>
<tr><td><a href='http://kaz29.hatenablog.com/entry/2013/04/30/122642' target='_blank'>「CIを半年間まわしてみて」というお題でLTをしてきました - kaz29</a></td><td>244</td><td>2013/04/30</td></tr>
</table>

<h3>5月:ベンチマークに関する記事とPaaS</h3>
5月で目を引くのはベンチマークに関する記事とGoogle AppEngineのPHP対応の記事でしょう。ベンチマークについては随時情報が更新されており、PHPはどちらかというと遅い部類に分類されていますがPhalconが特に高いパフォーマンスを出しており注目されました。以降、実際にPhalconを使っているという話題や使ってみたいという声の引き金になった話題と言ってよいでしょう。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://www.moongift.jp/2013/05/20130506/' target='_blank'>MySQL/SQLiteのER図を描くPHPスクリプト「mysqlviz」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td><td>144</td><td>2013/05/06</td></tr>
<tr><td><a href='http://tech.a-listers.jp/2013/05/06/web-framework-benchmark/' target='_blank'>16の言語と57のフレームワークを比較したベンチマークが凄い | A-Listers</a></td><td>555</td><td>2013/05/06</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/kazuk_i/20130508/1368018346' target='_blank'>弊社エンジニア職の求人に、日本から一向に応募が無い件 - Tous Les Jours 攻防記</a></td><td>434</td><td>2013/05/08</td></tr>
<tr><td><a href='http://anond.hatelabo.jp/20130513092207' target='_blank'>素人がそこそこのWebサービスをつくる方法</a></td><td>598</td><td>2013/05/13</td></tr>
<tr><td><a href='http://rosylilly.hatenablog.com/entry/2013/05/13/231447' target='_blank'>プログラミングの話 - 鳩舎</a></td><td>213</td><td>2013/05/13</td></tr>
<tr><td><a href='https://speakerdeck.com/tdak/yurukawalinux' target='_blank'>ゆるかわLinux // Speaker Deck</a></td><td>109</td><td>2013/05/14</td></tr>
<tr><td><a href='http://monosy.com/blog/1' target='_blank'>ゆとり文系も一人でWebサービスを作ってみました｜Monosyブログ</a></td><td>648</td><td>2013/05/15</td></tr>
<tr><td><a href='http://www.publickey1.jp/blog/13/google_app_enginephpphpsdk.html' target='_blank'>Google App EngineがPHPに対応、限定プレビューを開始。ローカルでPHP環境を再現するSDKも公開 － Publickey</a></td><td>219</td><td>2013/05/17</td></tr>
<tr><td><a href='http://anond.hatelabo.jp/20130517213002' target='_blank'>アフィリエイトで勘違いした大学生の末路</a></td><td>613</td><td>2013/05/17</td></tr>
<tr><td><a href='http://uiureo.hatenablog.com/entry/2013/05/19/030414' target='_blank'>GIFアニメ生成にImageMagickはオワコン、情強は高速なGraphicsMagickを使う - 海峡</a></td><td>473</td><td>2013/05/19</td></tr>
<tr><td><a href='http://plus.find-job.net/programming-learning-site' target='_blank'>手遅れになる前に！Webディレクターがプログラミングを学ぶ時に使いたいサイト10選</a></td><td>948</td><td>2013/05/20</td></tr>
<tr><td><a href='http://blog.tokumaru.org/2013/05/JSON-information-disclosure-vulnerability-CVE-2013-1297.html' target='_blank'>JSONをvbscriptとして読み込ませるJSONハイジャック(CVE-2013-1297)に注意 | 徳丸浩の日記</a></td><td>237</td><td>2013/05/20</td></tr>
<tr><td><a href='http://www.atmarkit.co.jp/ait/articles/1305/23/news004.html' target='_blank'>NoSQLを使うなら知っておきたいセキュリティの話（1）：「演算子のインジェクション」と「SSJI」 (1/2) - ＠IT</a></td><td>216</td><td>2013/05/22</td></tr>
<tr><td><a href='http://liginc.co.jp/web/tool/30371' target='_blank'>意外と知らない？サイトの更新が便利なCMSまとめ15選 | 株式会社LIG</a></td><td>200</td><td>2013/05/23</td></tr>
<tr><td><a href='http://phpspot.org/blog/archives/2013/05/phprubyjshtmlcs.html' target='_blank'>PHP,Ruby,JS,HTML,CSSをブラウザ上で開発できるオープンソースIDEエディタ「ICEcoder」:phpspot開発日誌</a></td><td>199</td><td>2013/05/24</td></tr>
<tr><td><a href='http://knoh.jp/answers/d65c7a82' target='_blank'>Evan Priestley 氏がどうやってプログラミングを学んだかを教えてください | Knoh</a></td><td>347</td><td>2013/05/28</td></tr>
<tr><td><a href='http://codezine.jp/article/detail/7141' target='_blank'>PHP::Haruで基本的なPDFを作成する （1/3）：CodeZine</a></td><td>159</td><td>2013/05/28</td></tr>
<tr><td><a href='http://monosy.com/blog/4' target='_blank'>Webサイトを作りたい人へ。一歩踏み出すために知りたい3つのこと｜Monosyブログ</a></td><td>109</td><td>2013/05/29</td></tr>
</table>

<h3>6月:学習への関心</h3>
6月の記事は個別のトピックというよりも体験談や学習方法といった内容が多いです。見返してみると今年はどのように学習しどのように使うのかといった話題やオンラインで学習できるコンテンツへの言及が多かったように思います。
実際に勉強会などでお会いする方でもドットインストールで勉強しているというような方に会う機会が増えたなと感じました。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://www.slideshare.net/cloned/php-kansai2013-lt' target='_blank'>一人でゲームをリリースするための自動化 PHPUnit編 ~目指せCoverage 100%~</a></td><td>102</td><td>2013/06/02</td></tr>
<tr><td><a href='http://anond.hatelabo.jp/20130608120106' target='_blank'>アマゾン商品をいい感じに検索できる「あまけん」をリリースしました</a></td><td>100</td><td>2013/06/08</td></tr>
<tr><td><a href='http://ginpen.com/2013/06/17/start-dash/' target='_blank'>Dashを入れてみたらjQueryやらのドキュメントを見るのが想像以上に快適だったよ。 | Ginpen.com</a></td><td>135</td><td>2013/06/17</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/yutakikuchi/20130617/1371425713' target='_blank'>誰もが一度は陥る日付処理。各種プログラミング言語におけるDateTime型/TimeStamp型の変換方法のまとめ - Yuta.Kikuchiの日記</a></td><td>620</td><td>2013/06/17</td></tr>
<tr><td><a href='http://blog.asial.co.jp/1175' target='_blank'>PHPで仮想マシンベースの正規表現エンジンを作ってみる 第一回 : アシアルブログ</a></td><td>136</td><td>2013/06/20</td></tr>
<tr><td><a href='http://blog.generace.co.jp/2013/06/21/894' target='_blank'>あなたのコード、激遅ぷんぷん丸？今すぐできる7つのチェック項目 PHP編 | GeNERACE labo</a></td><td>252</td><td>2013/06/21</td></tr>
<tr><td><a href='http://www.slideshare.net/luminhacker/web-23310333' target='_blank'>Webクローリング＆スクレイピングの最前線 公開用</a></td><td>472</td><td>2013/06/22</td></tr>
<tr><td><a href='http://tech.basicinc.jp/PHP/2013/06/17/vim-php/' target='_blank'>VimをPHP用にカスタマイズする - vim使いこなしたいvim初心者へ</a></td><td>210</td><td>2013/06/23</td></tr>
<tr><td><a href='http://yoonchulkoh.hatenablog.com/entry/2013/06/25/083305' target='_blank'>新卒エンジニアのための先輩エンジニアによる一目置かれるエンジニアとして成長していくために必要なこと。 - 悪あがきプログラマー</a></td><td>476</td><td>2013/06/25</td></tr>
<tr><td><a href='http://creive.me/archives/2896/' target='_blank'>「学びたい、全ての人へ」creiveより</a></td><td>2000</td><td>2013/06/30</td></tr>
<tr><td><a href='http://www.100shiki.com/archives/2013/06/learn_x_in_y_minutes.html' target='_blank'>プログラミング言語を最速で学ぶための『Learn X in Y minutes』 | 100SHIKI</a></td><td>169</td><td>2013/06/30</td></tr>
</table>

<h3>7月:Vagrant、Phalcon、浮動小数点</h3>
7月あたりからはPHPの開発にVagrantを使うという話題を聞くことが増えてきます。実際にPHPカンファレンス関西などでの講演を受けて試してみようという人が増えてきたのでしょう。またPhalconについてまとまった資料が出てきた事で注目が集まりました。
一方で浮動小数点というPHPにとっては伝統芸といってもよい話題も出てきています。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://www.moongift.jp/2013/07/20130706-2/' target='_blank'>これは凄い！iOSアプリ内で動作するPHP「iPHP」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td><td>393</td><td>2013/07/06</td></tr>
<tr><td><a href='http://www.find-job.net/startup/api-2013' target='_blank'>日本の全エンジニアに捧ぐ！現在公開されているAPI一覧【2013年版】 | Find Job ! Startup</a></td><td>3837</td><td>2013/07/10</td></tr>
<tr><td><a href='http://webnaut.jp/markup/606.html' target='_blank'>【業務効率が変わる！】こんな時に役に立つ「正規表現」の使い所 | Markup | WebNAUT</a></td><td>270</td><td>2013/07/11</td></tr>
<tr><td><a href='http://www.moongift.jp/2013/07/20130715/' target='_blank'>データベース無し、Markdownでコンテンツを作成するCMS「Pico」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td><td>192</td><td>2013/07/15</td></tr>
<tr><td><a href='http://btwael.github.io/mammouth/' target='_blank'>Mammouth</a></td><td>117</td><td>2013/07/15</td></tr>
<tr><td><a href='http://phpspot.org/blog/archives/2013/07/grepgrepack.html' target='_blank'>grepをよく使うプログラマはどう考えても乗り換えるべき新しいgrepコマンド「ack」:phpspot開発日誌</a></td><td>325</td><td>2013/07/16</td></tr>
<tr><td><a href='http://www.infiniteloop.co.jp/blog/2013/07/phpmatsuri-db-partition/' target='_blank'>PHPMatsuri2013で発表した資料を公開しました「ソーシャルゲーム案件におけるDB分割のPHP実装～とにかく分割ですよ。10回じゃ足りない。20回くらい分割。～」 | 株式会社インフィニットループ</a></td><td>131</td><td>2013/07/16</td></tr>
<tr><td><a href='http://www.slideshare.net/shin1x1/xampp-mamp-vagrant-php' target='_blank'>もう XAMPP / MAMP はいらない！ Vagrant で作る PHP 開発環境</a></td><td>733</td><td>2013/07/18</td></tr>
<tr><td><a href='http://blog.livedoor.jp/itsoku/archives/30593028.html' target='_blank'>２ｃｈの天才「YouTube動画をリアルタイムで共有できるチャットつくったった」 : IT速報</a></td><td>525</td><td>2013/07/18</td></tr>
<tr><td><a href='http://melpon.org/wandbox/' target='_blank'>wandbox</a></td><td>135</td><td>2013/07/19</td></tr>
<tr><td><a href='http://commte.net/blog/archives/3403' target='_blank'>ひとりでWeb制作できた！「知識０から学ぶ」すごいスライドやサイト２７ | コムテブログ</a></td><td>1408</td><td>2013/07/22</td></tr>
<tr><td><a href='http://k1low.hatenablog.com/entry/2013/07/22/185615' target='_blank'>さくらVPSセットアップ用のシェルスクリプトを今話題の「Ansible」で書き直してみた - Copy/Cut/Paste/Hatena</a></td><td>262</td><td>2013/07/22</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/hnw/20130723' target='_blank'>第70回PHP勉強会で浮動小数点数の話をしました - hnwの日記</a></td><td>102</td><td>2013/07/23</td></tr>
<tr><td><a href='http://www.ideaxidea.com/archives/2013/07/jennifer_dewalt.html' target='_blank'>プログラミング経験ゼロから『180日連続で毎日1個サイト作るぞ！』を実践しているJenifferさんの作品群がすごい | IDEA*IDEA</a></td><td>706</td><td>2013/07/25</td></tr>
<tr><td><a href='http://www.rodeo.jp.net/tech/phalcon-php-framework/' target='_blank'>RODEO.inc » 爆速フレームワーク!! Phalcon PHP Framework</a></td><td>142</td><td>2013/07/26</td></tr>
<tr><td><a href='http://shgam.hatenadiary.jp/entry/2013/07/24/181230' target='_blank'>Webサービス作るの難しすぎるよう... - 文系学生のプログラミング入門</a></td><td>222</td><td>2013/07/28</td></tr>
</table>

<h3>8月:モダンPHPとムック本</h3>
8月はLLまつりで行ったモダンPHPチュートリアルの記事と資料が話題になりました。このセッションではComposerの利用を強く勧めていますが、Composerも今年特に利用が進んだツールでしょう。またそういったさまざまなノウハウをまとめた「PHPエンジニア養成読本」が出版され、今年出版されたPHPの書籍の中でも特に注目が集まりました。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://commte.net/blog/archives/3459' target='_blank'>ここまで出来る！覚えとくと便利な「プログラム」サンプルまとめ | コムテブログ</a></td><td>299</td><td>2013/08/05</td></tr>
<tr><td><a href='http://blog.tokumaru.org/2013/08/1.html' target='_blank'>パスワードの定期的変更について徳丸さんに聞いてみた(1) | 徳丸浩の日記</a></td><td>564</td><td>2013/08/05</td></tr>
<tr><td><a href='http://codeiq.hatenablog.com/entry/2013/08/07/162935' target='_blank'>『PHPでオブジェクト指向的FizzBuzz』問題の解説記事～PHPが書けてオブジェクト指向がわかるとイケてるエンジニアになれる!? #php #オブジェクト指向 - CodeIQ Blog</a></td><td>302</td><td>2013/08/07</td></tr>
<tr><td><a href='http://www.slideshare.net/takyam1213/php-meets-nodejs' target='_blank'>PHP meets NodeJS</a></td><td>104</td><td>2013/08/12</td></tr>
<tr><td><a href='http://code-plus.jp/tools/sublime-text-2-plugin/' target='_blank'>使用中のSublime Text 2のプラグインをまとめてみた | CodePlus</a></td><td>153</td><td>2013/08/15</td></tr>
<tr><td><a href='http://stocker.jp/diary/useful-usage-of-php/' target='_blank'>Webデザイナーやコーダーの方でも知っておきたいPHPの便利な使い方 | Stocker.jp / diary</a></td><td>516</td><td>2013/08/20</td></tr>
<tr><td><a href='http://www.atmarkit.co.jp/ait/articles/1308/20/news004.html' target='_blank'>PHP 5.5の新機能：さっくり理解するPHP 5.5の言語仕様と「いい感じ」の使い方 (1/2) - ＠IT</a></td><td>244</td><td>2013/08/20</td></tr>
<tr><td><a href='http://blog.livedoor.jp/darkm/archives/51507584.html' target='_blank'>サイトを作って２ヶ月でサイト収入が2万/月になった話 : はれぞう</a></td><td>288</td><td>2013/08/21</td></tr>
<tr><td><a href='http://www.slideshare.net/ockeghem/ss-25447896' target='_blank'>いまさら聞けないパスワードの取り扱い方</a></td><td>587</td><td>2013/08/21</td></tr>
<tr><td><a href='http://plus.vc/web/php/6850/' target='_blank'>入力フォームの迷宮。全角数字を強要するフォームを理解できません。 | PLUS</a></td><td>282</td><td>2013/08/22</td></tr>
<tr><td><a href='https://speakerdeck.com/yandod/modanphptiyutoriaru-llmaturiban' target='_blank'>モダンPHPチュートリアル (LLまつり版) // Speaker Deck</a></td><td>368</td><td>2013/08/24</td></tr>
<tr><td><a href='http://www.slideshare.net/ockeghem/xssreintroduction' target='_blank'>XSS再入門</a></td><td>422</td><td>2013/08/26</td></tr>
<tr><td><a href='http://www.engineyard.co.jp/blog/2013/modern-php-tutorial/' target='_blank'>モダンPHPチュートリアルを開催しました | Engine Yard Blog JP</a></td><td>133</td><td>2013/08/26</td></tr>
<tr><td><a href='http://webnaut.jp/markup/628.html' target='_blank'>一度書いたコードは二度と探さない！スニペットを究めて快適コーディング！【HTML, CSS, JavaScript】 | Markup | WebNAUT</a></td><td>715</td><td>2013/08/26</td></tr>
<tr><td><a href='http://blog.glidenote.com/blog/2013/08/26/ojt-with-wemux/' target='_blank'>新卒OJTにwemux(multi-user terminal multiplexing)を使って画面共有することにした - Glide Note - グライドノート</a></td><td>255</td><td>2013/08/26</td></tr>
<tr><td><a href='http://arukeba.jp/everbeautify.html' target='_blank'>ソースコードをEvernoteに保存するならEverbeautifyがオススメ！PHPもRubyもPythonも、どんと来い！ | 歩けば僕の足跡</a></td><td>162</td><td>2013/08/27</td></tr>
<tr><td><a href='http://blog.wktk.co.jp/ja/entry/2013/08/27/diff-of-maru-moritapo' target='_blank'>2chの情報流出にあたって、●とモリタポとbe2ちゃんねるの違い</a></td><td>232</td><td>2013/08/27</td></tr>
<tr><td><a href='http://mawatari.jp/archives/backbonejs-todos-with-cakephp-restful-api' target='_blank'>CakePHPでRESTful APIを作って、Backbone.jsのデータの永続化をサーバサイドで行う | mawatari.jp</a></td><td>101</td><td>2013/08/27</td></tr>
<tr><td><a href='http://www.msng.info/archives/2013/08/php-engineer-book.php' target='_blank'>いまどきのPHP開発ノウハウを詰め込んだ『PHPエンジニア養成読本』が出るので、見所をまとめてみるよ - 頭ん中</a></td><td>297</td><td>2013/08/27</td></tr>
<tr><td><a href='http://ssl.japanknowledge.jp/hougen/' target='_blank'>出身地鑑定!! 方言チャート</a></td><td>1166</td><td>2013/08/27</td></tr>
<tr><td><a href='http://qiita.com/mpyw/items/b00b72c5c95aac573b71' target='_blank'>PHPでデータベースに接続するときのまとめ - Qiita [キータ]</a></td><td>672</td><td>2013/08/28</td></tr>
<tr><td><a href='http://blog.webcreativepark.net/2013/08/28-010250.html' target='_blank'>Gruntで始めるWeb制作の自動化 - to-R</a></td><td>232</td><td>2013/08/28</td></tr>
<tr><td><a href='http://lolipop.jp/info/news/4149/' target='_blank'>【最重要】ロリポップ！レンタルサーバーで発生している不正ログインについて / 新着情報 / お知らせ - レンタルサーバーならロリポップ！</a></td><td>175</td><td>2013/08/29</td></tr>
<tr><td><a href='http://www.moongift.jp/2013/08/20130829-3/' target='_blank'>PHP専用のデバッグツールバー「DebugBar」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td><td>104</td><td>2013/08/29</td></tr>
<tr><td><a href='http://wonderpla.net/blog/engineer/Vim_plugin' target='_blank'>開発言語に関わらず入れとくべきVimプラグイン3つ | ワンダープラネットエンジニア Blog</a></td><td>100</td><td>2013/08/29</td></tr>
<tr><td><a href='http://k-holy.hatenablog.com/entry/2013/08/30/192243' target='_blank'>Windows7にVirtualBoxとVagrantをインストールしたメモ - k-holyのPHPとか諸々メモ</a></td><td>197</td><td>2013/08/30</td></tr>
</table>

<h3>9月:セキュリティ問題とカンファレンス</h3>
8月の末にWordPressを利用しているユーザをターゲットにした大規模な攻撃が行われ、その問題についての考察が話題を呼びました。また9月にはPHPカンファレンスが開催されさまざまな資料が公開されました。PHPカンファレンスについてはこちらのページに資料が集まっています。

<a href="http://lanyrd.com/2013/php-conference-japan/"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/PHP_Conference_Japan_2013__14th_September_2013___Lanyrd-2-1024x678.png" alt="PHP_Conference_Japan_2013__14th_September_2013___Lanyrd-2" width="1024" height="678" class="alignnone size-large wp-image-2202" /></a>

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://blog.tokumaru.org/2013/09/symlink-attack.html' target='_blank'>ロリポップのサイト改ざん事件に学ぶシンボリックリンク攻撃の脅威と対策 | 徳丸浩の日記</a></td><td>954</td><td>2013/09/02</td></tr>
<tr><td><a href='http://tanaka.sakura.ad.jp/2013/09/symlink-attack.html' target='_blank'>共用サーバにおけるSymlink Attacksによる攻撃とその対策について - さくらインターネット創業日記</a></td><td>648</td><td>2013/09/03</td></tr>
<tr><td><a href='http://phpy.readthedocs.org/en/latest/' target='_blank'>php プログラマのための Python チュートリアル — phpy 0.1 documentation</a></td><td>217</td><td>2013/09/06</td></tr>
<tr><td><a href='http://careerbaito.com/column/detail/570' target='_blank'>PHPを始めたばかりの学生へ！代表的な7つのPHPフレームワークの違いと特徴｜キャリアバイトコラム</a></td><td>506</td><td>2013/09/13</td></tr>
<tr><td><a href='http://www.slideshare.net/cubicdaiya/inside-pixiv-infrastructure' target='_blank'>Inside pixiv's infrastructure〜application cluster side〜</a></td><td>154</td><td>2013/09/14</td></tr>
<tr><td><a href='http://www.slideshare.net/yoku0825/devsdba' target='_blank'>Devsの常識、DBAは非常識</a></td><td>626</td><td>2013/09/14</td></tr>
<tr><td><a href='http://www.slideshare.net/ockeghem/phpconf2013' target='_blank'>安全なPHPアプリケーションの作り方2013</a></td><td>675</td><td>2013/09/14</td></tr>
<tr><td><a href='http://blog.kentarok.org/entry/2013/09/14/205810' target='_blank'>「PHPアプリケーションの継続的バージョンアップ」という題でPHPカンファレンス2013でトークしてきた #phpcon2013 - delirious thoughts</a></td><td>175</td><td>2013/09/14</td></tr>
<tr><td><a href='https://speakerdeck.com/kuromatu/rubykaraphphe-enziniafalsetamefalsesi-kao-yi-xing-gaido' target='_blank'>RubyからPHPへ -エンジニアのための思考移行ガイド- // Speaker Deck</a></td><td>103</td><td>2013/09/14</td></tr>
<tr><td><a href='https://speakerdeck.com/ken_c_lo/pull-request-4-designers-githubwoshi-tutapuroguramatodezainafalseitereteibunakai-fa-huro' target='_blank'>Pull Request 4 Designers - GitHubを使ったプログラマとデザイナーのイテレーティブな開発フロー // Speaker Deck</a></td><td>140</td><td>2013/09/15</td></tr>
<tr><td><a href='http://unsolublesugar.com/20130915/005329/' target='_blank'>PHPカンファレンス2013 & WordCamp Tokyo 2013 講演資料まとめ #phpcon2013 #wctokyo | Time to live forever</a></td><td>123</td><td>2013/09/15</td></tr>
<tr><td><a href='http://sho.tdiary.net/20130915.html#p01' target='_blank'>HTTPでHashやArrayを送る手法に仕様は存在しない……の? - ただのにっき(2013-09-15)</a></td><td>151</td><td>2013/09/16</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/ozuma/20130916/1379332757' target='_blank'>phpMyAdminを狙った攻撃観察 - ろば電子が詰まっている</a></td><td>122</td><td>2013/09/16</td></tr>
<tr><td><a href='http://www.1x1.jp/blog/2013/09/php-enviroment-with-vagrant.html' target='_blank'>Vagrantで作るPHP開発環境[実践編]をPHPカンファレンス2013で発表してきた - Shin x blog</a></td><td>223</td><td>2013/09/17</td></tr>
<tr><td><a href='http://www.slideshare.net/techblogyahoo/phpcon2013-performance' target='_blank'>本当に怖いパフォーマンスが悪い実装 #phpcon2013</a></td><td>458</td><td>2013/09/17</td></tr>
<tr><td><a href='http://blog.livedoor.jp/itsoku/archives/33268831.html' target='_blank'>2ちゃんねらー‎「PHPでアプリのまとめサイト作ったんだが・・・・」 : IT速報</a></td><td>102</td><td>2013/09/23</td></tr>
<tr><td><a href='http://www.publickey1.jp/blog/13/facebookmysqlmysql_connect_2013.html' target='_blank'>FacebookにおけるMySQLを用いた大規模システムアーキテクチャの現実～MySQL Connect 2013 － Publickey</a></td><td>485</td><td>2013/09/27</td></tr>
<tr><td><a href='http://2013.8-p.info/japanese/09-28-languages.html' target='_blank'>はじめの言語の賞味期限 - Kato Kazuyoshi</a></td><td>359</td><td>2013/09/28</td></tr>
<tr><td><a href='http://blog.tokumaru.org/2013/09/cookie-manipulation-is-possible-even-on-ssl.html' target='_blank'>HTTPSを使ってもCookieの改変は防げないことを実験で試してみた | 徳丸浩の日記</a></td><td>611</td><td>2013/09/30</td></tr>
</table>

<h3>10月:オープンソースのメッセンジャーが話題に</h3>
PHPでバックエンドを実装したメッセンジャーアプリが公開され話題を呼んでいます。当初は炎上的な展開でしたがGitHubを利用してソーシャルにコードが改善され、またその際にはVagrantや継続的テスト、Composer、Symfonyなどのナレッジが効果的に活用されケーススタディとしても価値があるエピソードになりました。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://jp.techcrunch.com/2013/10/03/20131002runnable-wants-to-become-the-youtube-of-code/' target='_blank'>「プログラムコードのYouTube」を目指すRunnable。サンプルはサイト内で編集・実行可 | TechCrunch Japan</a></td><td>421</td><td>2013/10/03</td></tr>
<tr><td><a href='http://www.slideshare.net/yujiotani16/redis-26851700' target='_blank'>Redis勉強会資料</a></td><td>210</td><td>2013/10/04</td></tr>
<tr><td><a href='http://dekokun.github.io/posts/2013-10-06.html' target='_blank'>ISUCON予選にPHP実装で参加して3位になりましたーやったことなどまとめ</a></td><td>171</td><td>2013/10/06</td></tr>
<tr><td><a href='http://techwave.jp/archives/spika_launching.html' target='_blank'>世界初 メッセンジャーアプリ「Spika」を完全オープンソースで公開、フロントからバックエンドまで提供 【増田 @maskin】 | TechWave</a></td><td>450</td><td>2013/10/08</td></tr>
<tr><td><a href='http://www.1x1.jp/blog/2013/10/vagrant-lapp-sample.html' target='_blank'>PHP開発環境のサンプルVagrantfile - Shin x blog</a></td><td>266</td><td>2013/10/09</td></tr>
<tr><td><a href='http://www.moongift.jp/2013/10/20131013/' target='_blank'>フリーランサー/小規模向けのプロジェクト管理「Solo」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td><td>327</td><td>2013/10/13</td></tr>
<tr><td><a href='http://blog.tojiru.net/article/377526320.html' target='_blank'>PHPのinterfaceとは何か - 泥のように</a></td><td>270</td><td>2013/10/15</td></tr>
<tr><td><a href='http://nigohiroki.hatenablog.com/entry/2013/10/17/001754' target='_blank'>これからWeb系のベンチャーで起業しようと思っている人へ考慮しなければいけないリストを作成した - nigoblog</a></td><td>1185</td><td>2013/10/17</td></tr>
<tr><td><a href='http://www.find-job.net/startup/architecture-2013' target='_blank'>国内注目のWebサービスを支える言語・フレームワーク・アーキテクチャ一覧【2013年版】 | Find Job ! Startup</a></td><td>1167</td><td>2013/10/17</td></tr>
<tr><td><a href='http://hitch.jp/blog/pixiv/' target='_blank'>月間38億PVを6人でさばくpixivインフラチーム久保氏のパフォーマンス向上術 | Hitch Blog</a></td><td>211</td><td>2013/10/18</td></tr>
<tr><td><a href='http://cloverstudioceo.hatenablog.com/entry/2013/10/21/033700' target='_blank'>Spikaを公開して起こった事 - ヨーロッパで働く社長のブログ</a></td><td>311</td><td>2013/10/21</td></tr>
<tr><td><a href='http://mkkn.hatenablog.jp/entry/2013/04/13/212100' target='_blank'>いつまでPHPerはMVCを間違い続けるのか…? - どうにもならない日々@mkkn</a></td><td>274</td><td>2013/10/21</td></tr>
<tr><td><a href='http://www.publickey1.jp/blog/13/facebookphpjithhvm_2217cpulinux.html' target='_blank'>FacebookがPHPのJITコンパイラ「HHVM 2.2」リリース。17％のCPU効率改善。Linuxディストリビューション用パッケージを用意 － Publickey</a></td><td>140</td><td>2013/10/22</td></tr>
<tr><td><a href='http://www.slideshare.net/hinakano/json-schema' target='_blank'>JSON SchemaとPHP</a></td><td>213</td><td>2013/10/29</td></tr>
<tr><td><a href='http://bugrammer.hateblo.jp/entry/2013/10/30/013451' target='_blank'>一人でコードを書きなさんな - Line 1: Error: Invalid Blog('by Esehara' )</a></td><td>218</td><td>2013/10/30</td></tr>
</table>

<h3>11月:正しい手法への関心</h3>
11月は大規模なマイグレーションの事例やセキュリティ関連の話題に注目があつまりました。また採用市場というちょっとかわった観点の話題も登場しています。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://blog.tokumaru.org/2013/11/apache-magica-attack.html' target='_blank'>CGI版PHPに対する魔法少女アパッチマギカ攻撃を観測しました | 徳丸浩の日記</a></td><td>150</td><td>2013/11/01</td></tr>
<tr><td><a href='http://at-grandpa.hatenablog.jp/entry/2013/11/01/072636' target='_blank'>「MVCの勘違い」について、もう一度考えてみる - 圧倒亭グランパのブログ</a></td><td>639</td><td>2013/11/01</td></tr>
<tr><td><a href='http://f-shin.net/fsgarage/638' target='_blank'>MVCにおけるcontrollerクラスの役割は時代と共に変わって行く | F's Garage＠fshin2000</a></td><td>344</td><td>2013/11/02</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/hnw/20131102' target='_blank'>PHPのジェネレータはイテレータより速い - hnwの日記</a></td><td>118</td><td>2013/11/03</td></tr>
<tr><td><a href='http://www.slideshare.net/j_nakada/aws-27835913' target='_blank'>モバイルゲームにおけるAWSの泥臭い使い方</a></td><td>363</td><td>2013/11/03</td></tr>
<tr><td><a href='http://phpmentors.jp/post/66318980165/mock-behaviors-not-states' target='_blank'>PHPメンターズ -> 状態ではなく、振る舞いをモックせよ</a></td><td>131</td><td>2013/11/08</td></tr>
<tr><td><a href='http://f-shin.net/fsgarage/751' target='_blank'>PHP vs Ruby 把握できていない人材採用市場 | F's Garage＠fshin2000</a></td><td>147</td><td>2013/11/09</td></tr>
<tr><td><a href='http://mizchi.hatenablog.com/entry/2013/11/10/081026' target='_blank'>ウェブエンジニアの生存戦略 - mizchi's blog</a></td><td>642</td><td>2013/11/10</td></tr>
<tr><td><a href='http://blogos.com/forum/70150/response/508799/' target='_blank'>PHP vs Ruby 把握できていない人材採用市場へのKrihalo - ソフトウェア相談などさんの意見</a></td><td>138</td><td>2013/11/12</td></tr>
<tr><td><a href='http://www.slideshare.net/kwatch/db-28097225' target='_blank'>DBスキーマもバージョン管理したい！</a></td><td>491</td><td>2013/11/12</td></tr>
<tr><td><a href='http://www.engineyard.co.jp/blog/2013/vagrant-and-berkshelf/' target='_blank'>nanapi勉強会でVagrant + Berkshelfについて発表しました | Engine Yard Blog JP</a></td><td>109</td><td>2013/11/13</td></tr>
<tr><td><a href='http://blog.ohgaki.net/fastest-php-framework-phalcon' target='_blank'>PHP最速フレームワークPhalconのインストール</a></td><td>102</td><td>2013/11/14</td></tr>
<tr><td><a href='http://slywalker.hateblo.jp/entry/2013/11/15/115907' target='_blank'>#CakePHP 爆速でAPIを実装するチュートリアル - 忍び歩く男 - SLYWALKER</a></td><td>183</td><td>2013/11/15</td></tr>
<tr><td><a href='http://luccafort.hatenablog.com/entry/2013/11/15/013842' target='_blank'>我輩、激おこプンプン丸で御座候 - 坊主の日記</a></td><td>178</td><td>2013/11/15</td></tr>
<tr><td><a href='http://blog.ohgaki.net/json-escape' target='_blank'>JSONのエスケープ</a></td><td>219</td><td>2013/11/16</td></tr>
<tr><td><a href='http://dqn.sakusakutto.jp/2013/11/php51to54.html' target='_blank'>ソースコード20万行の大規模サイトのPHPを5.1から5.4に上げるためにやったことまとめ - DQNEO起業日記</a></td><td>568</td><td>2013/11/18</td></tr>
<tr><td><a href='https://codeiq.jp/magazine/2013/11/1475/' target='_blank'>これであなたもテスト駆動開発マスター！？和田卓人さんがテスト駆動開発問題を解答コード使いながら解説します～現在時刻が関わるテストから、テスト容易性設計を学ぶ #tdd｜CodeIQ MAGAZI</a></td><td>796</td><td>2013/11/26</td></tr>
<tr><td><a href='http://sclo.hatenablog.com/entry/2013/11/28/185901' target='_blank'>「将来に向けて節約をしながらも、今の暮らしを楽しむ方法」に、私、感動する。 - 僭越ながら</a></td><td>398</td><td>2013/11/28</td></tr>
<tr><td><a href='http://www.sophos.com/ja-jp/press-office/press-releases/2013/11/ns-serious-security-how-to-store-your-users-passwords-safely.aspx' target='_blank'>ユーザーのパスワードを安全に保管する方法について - 11 - 2013 - Sophos Press Releases, Security News and Press Coverage - Sophos Press Office | Sophos News and Press Releases - ソフォス</a></td><td>180</td><td>2013/11/28</td></tr>
<tr><td><a href='http://blog.tokumaru.org/2013/11/xsssqlrfc5322.html' target='_blank'>XSSとSQLインジェクションの両方が可能なRFC5322適合のメールアドレス | 徳丸浩の日記</a></td><td>438</td><td>2013/11/29</td></tr>
</table>

<h3>12月:新機能の利用が進む</h3>
12月も引き続きセキュリティ関連の話題などがありましたが、PHP5.5の新機能であるジェネレータについての記事が印象的です。カンファレンスなどでも機能の概要は紹介されていましたが、実際に利用する中で得た知見について耳にする機会が増えてきました。
PHP5.5もリリースから約半年が経過していますが、まだ利用していない方は早めの導入とジェネレータなどの新機能を効果的に活用する事をご検討ください。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://www.engineyard.co.jp/blog/2013/vagrantfile-for-php/' target='_blank'>PHPの開発に使えるVagrantfileのまとめ | Engine Yard Blog JP</a></td><td>235</td><td>2013/12/01</td></tr>
<tr><td><a href='http://www.msng.info/archives/2013/12/php-array-magic.php' target='_blank'>PHP の配列を使った手品とその種明かし - 頭ん中</a></td><td>149</td><td>2013/12/02</td></tr>
<tr><td><a href='http://c-note.chatwork.com/post/68781816704/phest-php-easy-static-site-generator' target='_blank'>黒い画面不要！デザイナ向け静的サイトジェネレーター「Phest」を公開しました</a></td><td>157</td><td>2013/12/03</td></tr>
<tr><td><a href='http://www.1x1.jp/blog/2013/12/recent_php_news_201312.html' target='_blank'>6分でわかる最近のPHP 2013年冬 - Shin x blog</a></td><td>148</td><td>2013/12/04</td></tr>
<tr><td><a href='http://blog.livedoor.jp/itsoku/archives/35414119.html' target='_blank'>PHP勉強してアフィで稼ごうと掲示板作ってみた結果ｗｗｗｗｗｗ : IT速報</a></td><td>137</td><td>2013/12/06</td></tr>
<tr><td><a href='http://www.1x1.jp/blog/2013/12/varnish-cache.html' target='_blank'>とある CMS を使ったサイトに Varnish を導入した話 - Shin x blog</a></td><td>170</td><td>2013/12/06</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/yayugu/20131207/1386407295' target='_blank'>そして老害になる - yayuguのにっき</a></td><td>397</td><td>2013/12/07</td></tr>
<tr><td><a href='http://developer.cybozu.co.jp/tech/?p=6527' target='_blank'>yrmcds 1.0.0 をリリースしました | Cybozu Inside Out | サイボウズエンジニアのブログ</a></td><td>110</td><td>2013/12/09</td></tr>
<tr><td><a href='http://qiita.com/Hiraku/items/0db9a8fed4743c1f00a4' target='_blank'>PHP - コードをまとめる技術としてのイテレータとジェネレータ - Qiita [キータ]</a></td><td>201</td><td>2013/12/10</td></tr>
<tr><td><a href='http://nekogata.hatenablog.com/entry/2013/12/11/142939' target='_blank'>PHP はいつもわたしに新鮮な驚きを与えてくれる - 猫型の蓄音機は 1 分間に 45 回にゃあと鳴く</a></td><td>326</td><td>2013/12/11</td></tr>
<tr><td><a href='http://tanakahisateru.hatenablog.jp/entry/2013/12/12/012728' target='_blank'>PHPが糞言語なのはどう考えても参照をポインタだと思っているお前らが悪い - なんたらノート第三期ベータ</a></td><td>501</td><td>2013/12/12</td></tr>
<tr><td><a href='http://blog.tokumaru.org/2013/12/php12sql.html' target='_blank'>PHPとセキュリティの解説書12種類を読んでSQLエスケープの解説状況を調べてみた | 徳丸浩の日記</a></td><td>336</td><td>2013/12/13</td></tr>
<tr><td><a href='http://wp-d.org/2013/12/19/5456/' target='_blank'>2013年Web制作に使い始めてよかったツール・サービスまとめ 〜そして時は2014年へ〜 | WP-D</a></td><td>516</td><td>2013/12/19</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/thk/20131221' target='_blank'>「WEB+DB PRESS」で艦これで有名なDMMの開発体制の全貌が明らかに - 東洋黒客の凱旋</a></td><td>238</td><td>2013/12/22</td></tr>
</table>

まとめてみるといかに最新のトピックをキャッチアップし続けるのが大変なのかという気もしてきますが、このタイミングで一気に追いついて2014年に備えましょう。みなさん、良いお年を。

<hr/>
<a href="http://ey.io/noyakshave"><img src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png"></a>
