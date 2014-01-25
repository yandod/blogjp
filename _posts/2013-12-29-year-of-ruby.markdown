---
layout: post
status: publish
published: true
title: 2013年Rubyの話題を一挙に振り返るまとめ
author: Yu Kitazume
author_login: ykitazume
author_email: ykitazume@engineyard.com
wordpress_id: 2219
wordpress_url: http://www.engineyard.co.jp/blog/?p=2219
date: 2013-12-29 15:35:36.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/2013-11-07-15.21.37.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/2013-11-07-15.21.37-1024x768.jpg" alt="2013-11-07 15.21.37" width="1024" height="768" class="alignnone size-large wp-image-2269" /></a>
<em>サンフランシスコのEngine Yard オフィス</em>

<a href="http://www.engineyard.co.jp/blog/2013/year-of-chef/">Chef</a>、 <a href="http://www.engineyard.co.jp/blog/2013/year-of-php/">PHP</a>につづき、Rubyの今年2013年を今年人気を集めた記事をテーマ別にまとめました。<a href="http://b.hatena.ne.jp/">はてなブックマーク</a>の数と一緒に振り返っていきます。今年の2月24日にRuby20周年を迎え、<a href="http://www.ruby-lang.org/ja/news/2013/02/24/ruby-2-0-0-p0-is-released/">ruby-2.0.0がリリース</a>されました。他にもRails4のリリース、<a href="http://www.atmarkit.co.jp/ait/articles/1306/03/news057.html">RubyKaigiの再開</a>など多くのトピックがありました。

<strong>目次</strong>
<ul>
<li><a href="#cruby-relesed">Ruby20周年！そしてruby-2.0.0, ruby-2.1.0のリリース</a></li>
<li><a href="#cruby">言語実装への興味、ガベージコレクションほか</a></li>
<li><a href="#spread">Rubyのひろがり</a></li>
<li><a href="#rails">Rails4のリリースとRailsの成熟</a></li>
<li><a href="#testci">テスト、CI</a></li>
<li><a href="#newways">開発環境、手法、デザイン</a></li>
<li><a href="#start">チュートリアル、Ruby, Railsを始める</a></li>
<li><a href="#books">Ruby 話題の本</a></li>
<li><a href="#maked">作りました！</a></li>
<li><a href="#opp">新しいライブラリ</a></li>
<li><a href="#fluentd">ログ・マネージメント fluentd</a></li>
<li><a href="#tips">Tips! コーディング</a></li>
<li><a href="#clientbackend">クライアントサイドとバックエンド</a></li>
<li><a href="#env">Rubyを取り巻く環境、組織</a></li>
<li><a href="#func">TwitterがRubyからJVM 言語群へ。関数型言語のトレンド
</a></li>
</ul>



<h3 id="cruby-relesed">Ruby20周年！そしてruby-2.0.0, ruby-2.1.0のリリース</h3>
Rubyが20周年を迎え、その丁度記念日となる2月24日に<a href="http://www.ruby-lang.org/ja/news/2013/02/24/ruby-2-0-0-p0-is-released/">ruby-2.0.0-p0がリリース</a>。クリスマスには<a href="http://www.ruby-lang.org/ja/news/2013/12/25/ruby-2-1-0-is-released/">2.1.0がリリース</a>されました。そして、長らくお世話になったruby-1.8.7が引退しました。

<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://www.ruby-lang.org/ja/news/2013/02/24/ruby-2-0-0-p0-is-released/" target="_blank">Ruby 2.0.0-p0 リリース</a></td>
<td>400</td>
<td>2013/02/24/</td>
</tr>
<tr>
<td><a href="http://jp.rubyist.net/magazine/?0041-200Special" target="_blank">Rubyist Magazine - Ruby 2.0.0 リリース特集</a></td>
<td>123</td>
<td>2013/02/24</td>
</tr>
<tr>
<td><a href="http://mrkn.hatenablog.com/entry/2013/03/19/232728" target="_blank">大江戸 Ruby 会議03で、某レシピサイトの Ruby 1.9.3 対応で苦労した点を共有しました - mrkn's diary</a></td>
<td>186</td>
<td>2013/03/19</td>
</tr>
<tr>
<td><a href="http://www.infoq.com/jp/news/2013/09/ruby-2-1-gc-revamp" target="_blank">Ruby 2.1がガベージコレクションを変更，大規模システムでの批判に対処</a></td>
<td>142</td>
<td>2013/09/24</td>
</tr>
<tr>
<td><a href="http://www.ruby-lang.org/ja/news/2013/12/25/ruby-2-1-0-is-released/ " target="_blank">Ruby 2.1.0-p0 リリース</a></td>
<td>-</td>
<td>2013/12/25</td>
</tr>
<tr>
<td><a href="http://www.ruby-lang.org/ja/news/2013/06/30/we-retire-1-8-7/" target="_blank">Ruby 1.8.7 は引退しました</a></td>
<td>144</td>
<td>2013/06/30</td>
</tr>
</tbody>
</table>
<h3 id="cruby">言語実装への興味、ガベージコレクションほか</h3>
言語そのものの実装にも多くの興味が寄せました。Crubyのコミッターの方々のブログを中心に多くのブックマークが付けれれました。
<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://loveruby.net/ja/rhg/book/gc.html" target="_blank">第5章 ガ−ベージコレクション</a></td>
<td>179</td>
<td>2013/06/15</td>
</tr>
<tr>
<td><a href="http://shyouhei.tumblr.com/post/64498820681/10-ruby" target="_blank">卜部昌平のあまりreblogしないtumblr - '10年代のRubyコア用語集</a></td>
<td>287</td>
<td>2013/10/20</td>
</tr>
<tr>
<td><a href="http://wazanova.jp/post/65317231718/ruby-python" target="_blank">RubyとPythonの違いからガベージコレクタを理解する - ワザノバ | wazanova.jp</a></td>
<td>325</td>
<td>2013/10/28</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/authorNari/20131209/1386583244" target="_blank">パーフェクトなCRubyを目指して - 1行のバグ修正に潜む苦労 - - I am Cruby!</a></td>
<td>184</td>
<td>2013/12/09</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/kazuhooku/20131221/1387603305" target="_blank">「今日使われているプログラミング言語の多くは、なぜ1990年前後に誕生したものなのか」に関する一考察 - kazuhoのメモ置き場</a></td>
<td>346</td>
<td>2013/12/21</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/authorNari/20130317/1363476355" target="_blank">桐島、Rubyやめるってよ #odrk03 - I am Cruby!</a></td>
<td>281</td>
<td>2013/03/17</td>
</tr>
</tbody>
</table>
<h3 id="spread">Rubyのひろがり</h3>
iOSアプリ、任天堂3DS、OpenFlow、エクセル、結婚式からダジャレまでRubyで作られたものは様々な所に広がっています。さらにユーザも中学生から女優までさまざま。mruby, RubyMotionの話題も追加し、人気を集めたRubyでつくらたものを集めてみました。

<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/laiso+iphone/20130624/1372093093" target="_blank">Objective-Cを絶対書きたくない人向けのiOSアプリ開発ソリューションの総括 - laiso</a></td>
<td>605</td>
<td>2013/06/25</td>
</tr>
<tr>
<td><a href="http://www.slideshare.net/yuyarin/ll2013-yuyarin-distpptx" target="_blank">Rubyで創るOpenFlowネットワーク - LLまつり</a></td>
<td>181</td>
<td>2013/08/24</td>
</tr>
<tr>
<td><a href="http://blog.64p.org/entry/2013/01/04/114443" target="_blank">ちょっとした GUI アプリケーションをつくるのに MacRuby はよい選択肢となりうる - tokuhirom's blog.</a></td>
<td>175</td>
<td>2013/01/04</td>
</tr>
<tr>
<td><a href="http://blog.katsuma.tv/2013/01/siriproxy-iremocon.html" target="_blank">SiriProxyのプラグインとしてSiriで家電を操作するSiriProxy-iRemocon - blog.katsuma.tv</a></td>
<td>170</td>
<td>2013/01/05</td>
</tr>
<tr>
<td><a href="http://blog.64p.org/entry/2013/01/08/102032" target="_blank">MacRuby でメニューバーのステータスメニューに常駐するアプリを作るための雛形をつくりました! - tokuhirom's blog.</a></td>
<td>229</td>
<td>2013/01/08</td>
</tr>
<tr>
<td><a href="http://webos-goodies.jp/archives/migrating_to_amazon_s3_static_web_hosting.html" target="_blank">サイトを Amazon S3 に移行しました - WebOS Goodies</a></td>
<td>262</td>
<td>2013/01/10</td>
</tr>
<tr>
<td><a href="http://tutorial.rubymotion.jp/" target="_blank">RubyMotion Tutorial: Ruby で iOS アプリを作ろう</a></td>
<td>285</td>
<td>2013/03/03</td>
</tr>
<tr>
<td><a href="http://blog.supermomonga.com/articles/jruby/javafx-rawr.html" target="_blank">RubyでGUIアプリを作るならJRuby+JavaFX+Rawrで決まり！ | かなりすごいブログ</a></td>
<td>323</td>
<td>2013/08/10</td>
</tr>
<tr>
<td><a href="http://www.nintendo.co.jp/3ds/interview/streetpass_relay/vol1/index4.html" target="_blank">ニンテンドー3DS｜社長が訊く「すれちがい通信中継所」｜Nintendo</a></td>
<td>238</td>
<td>2013/09/06</td>
</tr>
<tr>
<td><a href="http://portal.nifty.com/kiji/130921161837_1.htm" target="_blank">@nifty：デイリーポータルZ：コンピューターにダジャレを教える</a></td>
<td>133</td>
<td>2013/09/22</td>
</tr>
<tr>
<td><a href="http://mamipeko.hatenablog.com/entry/happy-wedding-s" target="_blank">「ご結婚おめでとう」親友に贈ったコードとデザインの話 - はぁはぁブログ</a></td>
<td>620</td>
<td>2013/10/23</td>
</tr>
<tr>
<td><a href="http://melborne.github.io/2013/11/11/your-data-from-excel-to-the-web/" target="_blank">Excelデータを最速でWebアプリ(Heroku)にする１０のステップ</a></td>
<td>254</td>
<td>2013/11/11</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/naoya/20131205/1386237472" target="_blank">RubyMotion を1年以上使い続けてみての雑感 - naoyaのはてなダイアリー</a></td>
<td>408</td>
<td>2013/12/05</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/maeharin/20130110/p1" target="_blank">仕事中、一瞬の隙も見逃さずに情報収集できるRubyワンライナーとスクリプト - maeharinの日記</a></td>
<td>276</td>
<td>2013/01/10</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/maeharin/20130113/ruby_oneliner" target="_blank">Rubyワンライナー入門 - maeharinの日記</a></td>
<td>223</td>
<td>2013/01/13</td>
</tr>
<tr>
<td><a href="http://blog.masuidrive.jp/index.php/2013/01/24/diff-cruby-mruby/" target="_blank">軽量Ruby – mrubyとRubyの違い - @masuidrive blog</a></td>
<td>173</td>
<td>2013/01/25</td>
</tr>
<tr>
<td><a href="http://blog.matsumoto-r.jp/?p=3588" target="_blank">mrubyによるWebサーバの機能拡張支援機構を一緒に開発しませんか？</a></td>
<td>150</td>
<td>2013/07/01</td>
</tr>
<tr>
<td><a href="http://www.atmarkit.co.jp/ait/articles/1303/04/news119.html" target="_blank">Rails Girls Tokyo レポート：キラッキラな「Ruby on Rails」の世界へ――Rails Girls 25人が集結 - ＠IT</a></td>
<td>103</td>
<td>2013/03/04</td>
</tr>
<tr>
<td><a href="http://blog.layer8.sh/ja/2013/05/30/ruby-girl-01/" target="_blank">【インタビュー】女子大生Webデザイナーが独学でRubyプログラマーへ転身！Ruby認定試験Goldを2ヶ月で取得したコツ</a></td>
<td>146</td>
<td>2013/06/02</td>
</tr>
<tr>
<td><a href="http://itpro.nikkeibp.co.jp/article/NEWS/20130627/488123/" target="_blank">ニュース - 松江市が中学生Ruby教室用ソフト一式をGitHubで公開、テキストもCCで無償配布：ITpro</a></td>
<td>191</td>
<td>2013/06/27</td>
</tr>
<tr>
<td><a href="http://itpro.nikkeibp.co.jp/article/NEWS/20130807/497268/" target="_blank">ニュース - 中学生Ruby教室“Mac編”のテキストとサンプルプログラム、松江市が無償公開：ITpro</a></td>
<td>103</td>
<td>2013/08/07</td>
</tr>
<tr>
<td><a href="http://weekly.ascii.jp/elem/000/000/162/162420/" target="_blank">ガチでギークな女優、池澤あやかがアメブロからTumblrに移行したワケ｜Mac</a></td>
<td>192</td>
<td>2013/08/08</td>
</tr>
<tr>
<td><a href="http://next.rikunabi.com/tech/docs/ct_s03600.jsp?p=002298" target="_blank">Ｒｕｂｙの女神降臨！池澤あやかのプログラミング｜【Tech総研】</a></td>
<td>468</td>
<td>2013/02/28</td>
</tr>
</tbody>
</table>
<h3 id="rails">Rails4のリリースとRailsの成熟</h3>

Railsの話題はつきません。今年はRails4がリリースされ、たくさんのノウハウが共有されました。

<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://kray.jp/blog/must-know-about-turbolinks/" target="_blank">Rails 4のturbolinksについて最低でも知っておきたい事 | KRAY Inc</a></td>
<td>288</td>
<td>2013/03/11</td>
</tr>
<tr>
<td><a href="http://morizyun.github.io/blog/draper-ruby-gem-code-clear/" target="_blank">Draperで驚くほどRailsコードがわかりやすくなったよ！ - 酒と泪とRubyとRailsと</a></td>
<td>142</td>
<td>2013/04/10</td>
</tr>
<tr>
<td><a href="http://techlife.cookpad.com/2013/04/10/chanko200/" target="_blank">プロトタイプ開発用のRailsプラグイン「Chanko」を2.0.0にアップデートしました | クックパッド開発者ブログ</a></td>
<td>332</td>
<td>2013/04/10</td>
</tr>
<tr>
<td><a href="http://qa.atmarkit.co.jp/q/2923" target="_blank">Railsで作ったサービスの速度改善方法について教えて下さい - QA@IT</a></td>
<td>402</td>
<td>2013/05/15</td>
</tr>
<tr>
<td><a href="https://speakerdeck.com/mirakui/high-performance-rails-long-edition" target="_blank">High Performance Rails (long edition) // Speaker Deck</a></td>
<td>167</td>
<td>2013/05/31</td>
</tr>
<tr>
<td><a href="http://qa-it.tumblr.com/post/52191914259/rails" target="_blank">「壊れてねぇなら直すな」という発想はRailsにはないのかも - QA@IT公式ブログ</a></td>
<td>227</td>
<td>2013/06/05</td>
</tr>
<tr>
<td><a href="http://techlife.cookpad.com/2013/06/07/rubykaigi-high-performance-rails/" target="_blank">Rails アプリケーションのパフォーマンスについて RubyKaigi 2013 で発表しました | クックパッド開発者ブログ</a></td>
<td>280</td>
<td>2013/06/07</td>
</tr>
<tr>
<td><a href="http://qa.atmarkit.co.jp/q/3005" target="_blank">rails で params に対して複雑な処理をするときのベストプラクティスは？ - QA@IT</a></td>
<td>112</td>
<td>2013/06/20</td>
</tr>
<tr>
<td><a href="http://tomykaira.hatenablog.com/entry/2013/06/25/124043" target="_blank">Rails、あんたなんか嫌いよ - Rails での OO 設計について - tomykaira makes love with codes</a></td>
<td>490</td>
<td>2013/06/25</td>
</tr>
<tr>
<td><a href="http://weblog.rubyonrails.org/2013/6/25/Rails-4-0-final/" target="_blank">Riding Rails: Rails 4.0: Final version released!</a></td>
<td>140</td>
<td>2013/06/25</td>
</tr>
<tr>
<td><a href="http://tomykaira.hatenablog.com/entry/2013/07/05/231752" target="_blank">Rails のモデルはどうあるべきか - tomykaira makes love with codes</a></td>
<td>230</td>
<td>2013/07/05</td>
</tr>
<tr>
<td><a href="http://techracho.bpsinc.jp/morimorihoge/2013_07_12/12482" target="_blank">Rails3アプリケーション開発で良く使うgemまとめ | TechRacho</a></td>
<td>170</td>
<td>2013/07/12</td>
</tr>
<tr>
<td><a href="https://speakerdeck.com/masuidrive/ruby-and-railsfalsezui-xin-ji-shu-dong-xiang-to-jin-hou-falseyu-xiang" target="_blank">Ruby&amp;Railsの最新技術動向と 今後の予想 // Speaker Deck</a></td>
<td>291</td>
<td>2013/09/06</td>
</tr>
<tr>
<td><a href="http://www.slideshare.net/techscore/ruby-on-rails-40-26007378" target="_blank">Ruby on rails 4.0 勉強会資料</a></td>
<td>134</td>
<td>2013/09/09</td>
</tr>
<tr>
<td><a href="http://blog.inouetakuya.info/entry/20130923/1379930345" target="_blank">Rails 4 へ移行してあらためて大切だと思ったこと + 役に立ったリンクを全力まとめ - 彼女からは、おいちゃんと呼ばれています</a></td>
<td>309</td>
<td>2013/09/23</td>
</tr>
<tr>
<td><a href="http://oauth.jp/blog/2013/09/26/rails-session-cookie/" target="_blank">Rails SessionにCookieStore使った時の問題点 - OAuth.jp</a></td>
<td>119</td>
<td>2013/09/26</td>
</tr>
<tr>
<td><a href="http://blog.inouetakuya.info/entry/2013/10/20/132928" target="_blank">Rails でつくる API のドキュメントを自動生成してくれる autodoc がすごい - 彼女からは、おいちゃんと呼ばれています</a></td>
<td>242</td>
<td>2013/10/20</td>
</tr>
<tr>
<td><a href="http://qiita.com/yusabana/items/8ce54577d959bb085b37" target="_blank">Ruby - Rails4 今のところ最強なデバッグツール達 - Qiita [キータ]</a></td>
<td>285</td>
<td>2013/10/24</td>
</tr>
<tr>
<td><a href="http://docs.komagata.org/5138" target="_blank">俺の被害妄想でrailsが死ぬ時 - komagata</a></td>
<td>145</td>
<td>2013/10/27</td>
</tr>
<tr>
<td><a href="http://techracho.bpsinc.jp/baba/2013_11_02/14645" target="_blank">Ruby on Rails 4.0.1リリース！大量のバグ修正、3系からの移行も少し簡単になりました | TechRacho</a></td>
<td>200</td>
<td>2013/11/03</td>
</tr>
<tr>
<td><a href="http://www.slideshare.net/kwatch/db-28097225" target="_blank">DBスキーマもバージョン管理したい！</a></td>
<td>491</td>
<td>2013/11/12</td>
</tr>
<tr>
<td><a href="http://techracho.bpsinc.jp/hachi8833/2013_11_19/14738" target="_blank">肥大化したActiveRecordモデルをリファクタリングする7つの方法(翻訳) | TechRacho</a></td>
<td>276</td>
<td>2013/11/19</td>
</tr>
<tr>
<td><a href="http://rosylilly.hatenablog.com/entry/2013/12/03/184748" target="_blank">speed_gun で Rails のパフォーマンスを測定する - 鳩舎</a></td>
<td>131</td>
<td>2013/12/03</td>
</tr>
<tr>
<td><a href="http://qiita.com/joker1007/items/2a03500017766bdb0234" target="_blank">Ruby - てめえらのRailsはオブジェクト指向じゃねえ！まずはCallbackクラス、Validatorクラスを活用しろ！ - Qiita [キータ]</a></td>
<td>272</td>
<td>2013/12/04</td>
</tr>
<tr>
<td><a href="http://kray.jp/blog/must-know-about-turbolinks/" target="_blank">Rails 4のturbolinksについて最低でも知っておきたい事 | KRAY Inc</a></td>
<td>288</td>
<td>2013/03/11</td>
</tr>
<tr>
<td><a href="http://morizyun.github.io/blog/draper-ruby-gem-code-clear/" target="_blank">Draperで驚くほどRailsコードがわかりやすくなったよ！ - 酒と泪とRubyとRailsと</a></td>
<td>142</td>
<td>2013/04/10</td>
</tr>
<tr>
<td><a href="http://techlife.cookpad.com/2013/04/10/chanko200/" target="_blank">プロトタイプ開発用のRailsプラグイン「Chanko」を2.0.0にアップデートしました | クックパッド開発者ブログ</a></td>
<td>332</td>
<td>2013/04/10</td>
</tr>
<tr>
<td><a href="http://qa.atmarkit.co.jp/q/2923" target="_blank">Railsで作ったサービスの速度改善方法について教えて下さい - QA@IT</a></td>
<td>402</td>
<td>2013/05/15</td>
</tr>
<tr>
<td><a href="https://speakerdeck.com/mirakui/high-performance-rails-long-edition" target="_blank">High Performance Rails (long edition) // Speaker Deck</a></td>
<td>167</td>
<td>2013/05/31</td>
</tr>
<tr>
<td><a href="http://qa-it.tumblr.com/post/52191914259/rails" target="_blank">「壊れてねぇなら直すな」という発想はRailsにはないのかも - QA@IT公式ブログ</a></td>
<td>227</td>
<td>2013/06/05</td>
</tr>
<tr>
<td><a href="http://techlife.cookpad.com/2013/06/07/rubykaigi-high-performance-rails/" target="_blank">Rails アプリケーションのパフォーマンスについて RubyKaigi 2013 で発表しました | クックパッド開発者ブログ</a></td>
<td>280</td>
<td>2013/06/07</td>
</tr>
<tr>
<td><a href="http://qa.atmarkit.co.jp/q/3005" target="_blank">rails で params に対して複雑な処理をするときのベストプラクティスは？ - QA@IT</a></td>
<td>112</td>
<td>2013/06/20</td>
</tr>
<tr>
<td><a href="http://tomykaira.hatenablog.com/entry/2013/06/25/124043" target="_blank">Rails、あんたなんか嫌いよ - Rails での OO 設計について - tomykaira makes love with codes</a></td>
<td>490</td>
<td>2013/06/25</td>
</tr>
<tr>
<td><a href="http://weblog.rubyonrails.org/2013/6/25/Rails-4-0-final/" target="_blank">Riding Rails: Rails 4.0: Final version released!</a></td>
<td>140</td>
<td>2013/06/25</td>
</tr>
<tr>
<td><a href="http://tomykaira.hatenablog.com/entry/2013/07/05/231752" target="_blank">Rails のモデルはどうあるべきか - tomykaira makes love with codes</a></td>
<td>230</td>
<td>2013/07/05</td>
</tr>
<tr>
<td><a href="http://techracho.bpsinc.jp/morimorihoge/2013_07_12/12482" target="_blank">Rails3アプリケーション開発で良く使うgemまとめ | TechRacho</a></td>
<td>170</td>
<td>2013/07/12</td>
</tr>
<tr>
<td><a href="https://speakerdeck.com/masuidrive/ruby-and-railsfalsezui-xin-ji-shu-dong-xiang-to-jin-hou-falseyu-xiang" target="_blank">Ruby&amp;Railsの最新技術動向と 今後の予想 // Speaker Deck</a></td>
<td>291</td>
<td>2013/09/06</td>
</tr>
<tr>
<td><a href="http://www.slideshare.net/techscore/ruby-on-rails-40-26007378" target="_blank">Ruby on rails 4.0 勉強会資料</a></td>
<td>134</td>
<td>2013/09/09</td>
</tr>
<tr>
<td><a href="http://blog.inouetakuya.info/entry/20130923/1379930345" target="_blank">Rails 4 へ移行してあらためて大切だと思ったこと + 役に立ったリンクを全力まとめ - 彼女からは、おいちゃんと呼ばれています</a></td>
<td>309</td>
<td>2013/09/23</td>
</tr>
<tr>
<td><a href="http://oauth.jp/blog/2013/09/26/rails-session-cookie/" target="_blank">Rails SessionにCookieStore使った時の問題点 - OAuth.jp</a></td>
<td>119</td>
<td>2013/09/26</td>
</tr>
<tr>
<td><a href="http://blog.inouetakuya.info/entry/2013/10/20/132928" target="_blank">Rails でつくる API のドキュメントを自動生成してくれる autodoc がすごい - 彼女からは、おいちゃんと呼ばれています</a></td>
<td>242</td>
<td>2013/10/20</td>
</tr>
<tr>
<td><a href="http://qiita.com/yusabana/items/8ce54577d959bb085b37" target="_blank">Ruby - Rails4 今のところ最強なデバッグツール達 - Qiita [キータ]</a></td>
<td>285</td>
<td>2013/10/24</td>
</tr>
<tr>
<td><a href="http://docs.komagata.org/5138" target="_blank">俺の被害妄想でrailsが死ぬ時 - komagata</a></td>
<td>145</td>
<td>2013/10/27</td>
</tr>
<tr>
<td><a href="http://techracho.bpsinc.jp/baba/2013_11_02/14645" target="_blank">Ruby on Rails 4.0.1リリース！大量のバグ修正、3系からの移行も少し簡単になりました | TechRacho</a></td>
<td>200</td>
<td>2013/11/03</td>
</tr>
<tr>
<td><a href="http://www.slideshare.net/kwatch/db-28097225" target="_blank">DBスキーマもバージョン管理したい！</a></td>
<td>491</td>
<td>2013/11/12</td>
</tr>
<tr>
<td><a href="http://techracho.bpsinc.jp/hachi8833/2013_11_19/14738" target="_blank">肥大化したActiveRecordモデルをリファクタリングする7つの方法(翻訳) | TechRacho</a></td>
<td>276</td>
<td>2013/11/19</td>
</tr>
<tr>
<td><a href="http://rosylilly.hatenablog.com/entry/2013/12/03/184748" target="_blank">speed_gun で Rails のパフォーマンスを測定する - 鳩舎</a></td>
<td>131</td>
<td>2013/12/03</td>
</tr>
<tr>
<td><a href="http://qiita.com/joker1007/items/2a03500017766bdb0234" target="_blank">Ruby - てめえらのRailsはオブジェクト指向じゃねえ！まずはCallbackクラス、Validatorクラスを活用しろ！ - Qiita [キータ]</a></td>
<td>272</td>
<td>2013/12/04</td>
</tr>
<tr>
<td><a href="http://bussorenre.hatenablog.jp/entry/2013/02/13/022739" target="_blank">上級者向け：Ruby on Rails 勉強法 - ぶっそれんれ研究室</a></td>
<td>262</td>
<td>2013/02/13</td>
</tr>
<tr>
<td><a href="http://el.jibun.atmarkit.co.jp/rails/2013/01/post-6025.html" target="_blank">Rails Hub情報局: プログラミング地獄への道は“ベストプラクティス”で敷き詰められている</a></td>
<td>242</td>
<td>2013/01/17</td>
</tr>
</tbody>
</table>
<h3 id="testci">テスト、CI</h3>

開発は終わるものではなく、継続的に続けていくものに変わりました。効率よく効果的に開発していく必要があります。Ruby、Railsと切っても切り離せない、テスト、CIについて人気を集めた記事をまとめました。

<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://qiita.com/awakia/items/d880250adc8cdbe7a32f" target="_blank">RSpecのshouldはもう古い！新しい記法expectを使おう！ #Ruby #Rspec - Qiita</a></td>
<td>143</td>
<td>2013/03/25</td>
</tr>
<tr>
<td><a href="http://qiita.com/unosk/items/c2e2bbc31d97e92803dc" target="_blank">Rails4時代の高速テスト環境 Rspec+Guard+FactoryGirl+Spring[NEW!] - Qiita [キータ]</a></td>
<td>147</td>
<td>2013/09/17</td>
</tr>
<tr>
<td><a href="http://qiita.com/sawanoboly/items/48fe830d2ee3b6c87bf5" target="_blank">"Cucumber,ChefSpecとchefでテスト駆動のサーバ構築管理 #infrastructure #Cucumber #Ruby #chef #chefspec - Qiita"</a></td>
<td>120</td>
<td>2013/01/27</td>
</tr>
<tr>
<td><a href="http://www.atmarkit.co.jp/ait/articles/1302/20/news032.html" target="_blank">フレームワークで実践！ JavaScriptテスト入門（5）：Capybara-Webkit＋Cucumber＋Sinon.JSでJavaScriptのテストはここまで変わる (1/3) - ＠IT</a></td>
<td>176</td>
<td>2013/02/20</td>
</tr>
<tr>
<td><a href="http://dev.classmethod.jp/cloud/aws/install-gitlab-amazon-vpc/" target="_blank">社内 GitHub を実用的に構築！ Amazon VPC 環境に GitLab サーバを構築してみた ｜ クラスメソッド開発ブログ</a></td>
<td>152</td>
<td>2013/02/25</td>
</tr>
<tr>
<td><a href="http://magazine.rubyist.net/?0042-FromCucumberToTurnip" target="_blank">Rubyist Magazine - エンドツーエンドテストの自動化は Cucumber から Turnip へ</a></td>
<td>261</td>
<td>2013/05/29</td>
</tr>
<tr>
<td><a href="http://techlife.cookpad.com/2013/06/13/how-we-deal-with-examples-fail-sometime/" target="_blank">CI で稀に失敗してしまうテストへの対処方法 | クックパッド開発者ブログ</a></td>
<td>276</td>
<td>2013/06/13</td>
</tr>
<tr>
<td><a href="http://blog.livedoor.jp/sasata299/archives/51925482.html" target="_blank">Spring無しでRailsを使おうだなんて正気ですかッ！？ - (ﾟ∀ﾟ)o彡 sasata299's blog</a></td>
<td>111</td>
<td>2013/08/06</td>
</tr>
<tr>
<td><a href="http://morizyun.github.io/blog/the-rspec-book-review-rails/" target="_blank">Rspec/Capybara/Turnipの入門記事を全力でまとめてみた - 酒と泪とRubyとRailsと</a></td>
<td>156</td>
<td>2013/08/30</td>
</tr>
<tr>
<td><a href="https://speakerdeck.com/kenchan/tdd-will-always-be-in-your-heart" target="_blank">TDD will always be in your heart // Speaker Deck</a></td>
<td>112</td>
<td>2013/08/31</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/koba04/20131128/1385568428" target="_blank">Webアプリケーションのテストを書くときに考えていること - 車輪を再発明 / koba04の日記</a></td>
<td>387</td>
<td>2013/11/28</td>
</tr>
<tr>
<td><a href="http://r7kamura.github.io/2013/12/01/autodoc.html" target="_blank">Autodoc - r7kamura blog</a></td>
<td>128</td>
<td>2013/12/02</td>
</tr>
<tr>
<td><a href="http://labs.gree.jp/blog/2013/12/10084/" target="_blank">入門 Capistrano 3 ~ 全ての手作業を生まれる前に消し去りたい | GREE Engineers' Blog</a></td>
<td>274</td>
<td>2013/12/21</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/mikeda/20130608/1370661384" target="_blank">サーバのリソース使用状況レポートを作る - IT 東京 楽しいと思うこと</a></td>
<td>111</td>
<td>2013/06/08</td>
</tr>
<tr>
<td><a href="http://blog.glidenote.com/blog/2013/05/20/working-with-irc-bot/" target="_blank">IRC BOTを作って仕事をさせるようにした - Glide Note - グライドノート</a></td>
<td>196</td>
<td>2013/05/20</td>
</tr>
</tbody>
</table>
<h3 id="newways">開発環境、手法、デザイン</h3>

プログラマは常に開発環境、手法について疑問を持ち改善していきます。また、プログラマがデザインを学ぶというテーマも見られました。年末年始に自分の開発環境を見直すのもいいかもしれません。

<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/ken_c_lo/20130115/1358269474" target="_blank">東京Ruby会議10で、Rubyistのためのデザイン講座ワークショップやらせていただきました #p4d #tkrk10 - 納豆には卵を入れる派です。</a></td>
<td>116</td>
<td>2013/01/16</td>
</tr>
<tr>
<td><a href="https://speakerdeck.com/ken_c_lo/rubyistfalsetamefalsezuruidezainhanzuon-in-rubyhiroba-p4d-wakusiyotupu" target="_blank">Rubyistのためのズルいデザインハンズオン in RubyHiroba P4D ワークショップ // Speaker Deck</a></td>
<td>121</td>
<td>2013/06/02</td>
</tr>
<tr>
<td><a href="http://qiita.com/emadurandal/items/a60886152a4c99ce1017" target="_blank">Rails開発環境の構築（rbenvでRuby導入からBundler、Rails導入まで） #Rails #rbenv #Mac #macports #Ruby - Qiita</a></td>
<td>123</td>
<td>2013/01/29</td>
</tr>
<tr>
<td><a href="http://blog.kyanny.me/entry/2013/05/10/rbenv_%E3%81%AE%E3%83%A1%E3%82%AB%E3%83%8B%E3%82%BA%E3%83%A0" target="_blank">rbenv のメカニズム - @kyanny's blog</a></td>
<td>120</td>
<td>2013/05/10</td>
</tr>
<tr>
<td><a href="http://dev.classmethod.jp/etc/modern-dev-environment-by-homebrew/" target="_blank">Homebrew で作るモダンなフロントエンド開発環境 (Git + zsh + apache + MySQL + Ruby) ｜ Developers.IO</a></td>
<td>112</td>
<td>2013/09/30</td>
</tr>
<tr>
<td><a href="http://blog.wktk.co.jp/ja/entry/2013/10/30/gdbruby" target="_blank">CoreからRubyのバックトレースを表示するgdbruby.rbを作った</a></td>
<td>128</td>
<td>2013/10/31</td>
</tr>
<tr>
<td><a href="http://dev.classmethod.jp/etc/github-homesick-dotfiles/" target="_blank">GitHub と homesick を使って複数 Mac 間で dotfiles を同期する ｜ Developers.IO</a></td>
<td>174</td>
<td>2013/11/19</td>
</tr>
<tr>
<td><a href="http://www.moongift.jp/2013/01/20130113/" target="_blank">Rails開発を補助するGoogle Chrome機能拡張「RailsPanel」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td>
<td>110</td>
<td>2013/01/13</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/deeeki/20130301/modern_rails_dev" target="_blank">モダンなRails開発をしてみての振り返り - 130単位</a></td>
<td>159</td>
<td>2013/03/01</td>
</tr>
<tr>
<td><a href="http://qa-it.tumblr.com/post/42010504223/github-qa-it" target="_blank">GitHub時代の開発委託とは？ デブサミでQA@ITの事例の話をします - QA@IT公式ブログ</a></td>
<td>228</td>
<td>2013/02/01</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/naoya/20131013/1381651545" target="_blank">Webサービス開発現場から / 近頃の開発のやり方 ･･･ Github と Pull Request とコードレビュー - naoyaのはてなダイアリー</a></td>
<td>1201</td>
<td>2013/10/13</td>
</tr>
<tr>
<td><a href="http://slides.redmine.jp/" target="_blank">Redmine Slides — Redmineを知るためのスライド集</a></td>
<td>141</td>
<td>2013/10/15</td>
</tr>
<tr>
<td><a href="http://cflat-inc.hatenablog.com/entry/2013/10/15/214715" target="_blank">Redmine裏技！複雑なチケット管理をカスタムクエリで超簡単に - まるちゃんブログ</a></td>
<td>236</td>
<td>2013/10/15</td>
</tr>
</tbody>
</table>
<h3 id="start">チュートリアル、Ruby, Railsを始める</h3>
新しいことをはじめるために必要な情報、自分が始めた時に困ったこと、役に立ったことをまとめた記事も多く投稿されました。
<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="https://gist.github.com/hsbt/5318109" target="_blank">2013 年の新卒研修メニュー</a></td>
<td>391</td>
<td>2013/04/05</td>
</tr>
<tr>
<td><a href="http://blog.satooshi.jp/blog/2013/04/08/before-you-get-started-ruby-programming/" target="_blank">2013年新学期にRubyを始めるエンジニアが読むべきサイトまとめ - satooshi@blog</a></td>
<td>516</td>
<td>2013/04/10</td>
</tr>
<tr>
<td><a href="http://railstutorial-ja.herokuapp.com/index.html" target="_blank">Ruby on Rails Tutorial (第２版) - 日本語</a></td>
<td>464</td>
<td>2013/06/04</td>
</tr>
<tr>
<td><a href="http://railstutorial.jp/" target="_blank">Ruby on Rails チュートリアル：実例を使ってRailsを学ぼう - Michael Hartl (マイケル・ハートル)</a></td>
<td>657</td>
<td>2013/06/12</td>
</tr>
<tr>
<td><a href="http://creive.me/archives/2896/" target="_blank">「学びたい、全ての人へ」creiveより</a></td>
<td>2000</td>
<td>2013/06/30</td>
</tr>
<tr>
<td><a href="http://www.slideshare.net/shokai/130715-ruby-intro" target="_blank">Ruby初級入門</a></td>
<td>189</td>
<td>2013/07/16</td>
</tr>
<tr>
<td><a href="http://commte.net/blog/archives/3403" target="_blank">ひとりでWeb制作できた！「知識０から学ぶ」すごいスライドやサイト２７ | コムテブログ</a></td>
<td>1409</td>
<td>2013/07/22</td>
</tr>
<tr>
<td><a href="http://railstutorial.jp/?version=4.0" target="_blank">Ruby on Rails チュートリアル：実例を使ってRailsを学ぼう - Michael Hartl (マイケル・ハートル)</a></td>
<td>221</td>
<td>2013/07/26</td>
</tr>
<tr>
<td><a href="https://www.bloc.io/ruby-warrior/#/" target="_blank">RubyWarrior - Bloc</a></td>
<td>178</td>
<td>2013/07/28</td>
</tr>
<tr>
<td><a href="http://techacademy.jp/magazine/807" target="_blank">Ruby作者まつもとゆきひろ氏も動画で解説！NaCl運営のRuby学習サービス「ミニツク」をやってみた！ | TechAcademyマガジン</a></td>
<td>344</td>
<td>2013/08/06</td>
</tr>
<tr>
<td><a href="http://hiroyukim.hatenablog.jp/entry/2013/10/02/030629" target="_blank">Rubyの入門書でいいものを知りませんかね？という質問に対してどう答えるべきだったか？ - (ヽ´ω`)　</a></td>
<td>118</td>
<td>2013/10/02</td>
</tr>
<tr>
<td><a href="http://nigohiroki.hatenablog.com/entry/2013/10/17/001754" target="_blank">これからWeb系のベンチャーで起業しようと思っている人へ考慮しなければいけないリストを作成した - nigoblog</a></td>
<td>1185</td>
<td>2013/10/17</td>
</tr>
<tr>
<td><a href="http://sanjose.main.jp/home/2013/10/28/getting-started-with-rails/" target="_blank">初心者から3ヶ月でRailsアプリ開発を身に付けるための地道な3ステップ | Designing Myself</a></td>
<td>591</td>
<td>2013/10/29</td>
</tr>
<tr>
<td><a href="http://u-note.me/note/47486703" target="_blank">Ruby on Ralisをこれから学ぶ人が絶対に知ってくべき本・サイトまとめ | U-NOTE【ユーノート】- ビジネスマンのためのノウハウまとめを無料で</a></td>
<td>133</td>
<td>2013/10/29</td>
</tr>
<tr>
<td><a href="http://www.find-job.net/startup/ruby-books" target="_blank">これからRubyを勉強する人が絶対読んでおきたい書籍9冊＋α | Find Job ! Startup</a></td>
<td>608</td>
<td>2013/11/06</td>
</tr>
<tr>
<td><a href="https://gist.github.com/udzura/7548163" target="_blank">やわらかRuby</a></td>
<td>430</td>
<td>2013/11/20</td>
</tr>
<tr>
<td><a href="http://blog.supermomonga.com/articles/ruby/sugoi-learning-way.html" target="_blank">今年こそRubyを始めたいあなたに！ももんが流・最強のRuby学習法 | かなりすごいブログ</a></td>
<td>141</td>
<td>2013/12/01</td>
</tr>
<tr>
<td><a href="http://shgam.hatenadiary.jp/entry/2013/12/18/160438" target="_blank">Ruby on Railsでブログを作成するときに役立った情報まとめ - 文系学生のプログラミング入門</a></td>
<td>126</td>
<td>2013/12/18</td>
</tr>
<tr>
<td><a href="http://melborne.github.io/2013/12/24/why-not-start-ruby/" target="_blank">僕が考えた最速・最小投資でRubyを学ぶ方法またはステマ乙</a></td>
<td>620</td>
<td>2013/12/24</td>
</tr>
</tbody>
</table>
<h3 id="books">Ruby 話題の本</h3>

学ぶためのソースはウェブだけではありません。Rubyについて話題になった本とその感想も人気を集めました。

<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://tatsu-zine.com/books/naruhounix" target="_blank">なるほどUnixプロセス ー Rubyで学ぶUnixの基礎 - 達人出版会</a></td>
<td>550</td>
<td>2013/04/06</td>
</tr>
<tr>
<td><a href="http://www.oreilly.co.jp/books/9784873116150/" target="_blank">O'Reilly Japan - RとRubyによるデータ解析入門</a></td>
<td>254</td>
<td>2013/04/12</td>
</tr>
<tr>
<td><a href="http://tatsu-zine.com/books/scheme-in-ruby" target="_blank">つくって学ぶプログラミング言語 RubyによるScheme処理系の実装 - 達人出版会</a></td>
<td>278</td>
<td>2013/04/16</td>
</tr>
<tr>
<td><a href="http://hakobe932.hatenablog.com/entry/2013/04/28/210815" target="_blank">なるほどUnixプロセス読んだ - デーモン化のためのdouble fork - HAKOBE blog ♨</a></td>
<td>121</td>
<td>2013/04/28</td>
</tr>
<tr>
<td><a href="http://tatsu-zine.com/books/mruby" target="_blank">まつもとゆきひろ直伝　組込Ruby「mruby」のすべて 総集編【委託】 - 達人出版会</a></td>
<td>101</td>
<td>2013/06/29</td>
</tr>
<tr>
<td><a href="http://gihyo.jp/book/2013/978-4-7741-5879-2" target="_blank">パーフェクトRuby　：書籍案内｜技術評論社</a></td>
<td>118</td>
<td>2013/07/29</td>
</tr>
<tr>
<td><a href="http://sugamasao.hatenablog.com/entry/2013/08/11/121217" target="_blank">パーフェクトRubyという本を（共著で）書きました - すがブロ</a></td>
<td>204</td>
<td>2013/08/11</td>
</tr>
<tr>
<td><a href="http://tatsu-zine.com/books/railstutorial" target="_blank">Ruby on Rails チュートリアル: 実例を使ってRailsを学ぼう - 達人出版会</a></td>
<td>118</td>
<td>2013/11/21</td>
</tr>
<tr>
<td><a href="http://snoozer05.org/?date=20131129#p01" target="_blank">[naruhounix]『なるほどUnixプロセス』という本を出しました - but its up to us to change(2013-11-29)</a></td>
<td>113</td>
<td>2013/11/29</td>
</tr>
</tbody>
</table>
<h3 id="maked">作りました！</h3>
実践を大事にするプログラマー。ハッカソン、ゴールデンウィーク、休職中などに、作りその苦労や楽しかったことを共有した記事にもたくさんブックマークがされました。
<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://sue445.hatenablog.com/entry/2013/12/16/000011" target="_blank">Rubyでプリキュアを作った #cure_advent - くりにっき</a></td>
<td>151</td>
<td>2013/12/16</td>
</tr>
<tr>
<td><a href="http://havelog.ayumusato.com/develop/ruby/e555-rails_on_heroku_app.html" target="_blank">Rails + Heroku で俺専用RSSリーダー作った ::ハブろぐ</a></td>
<td>225</td>
<td>2013/03/31</td>
</tr>
<tr>
<td><a href="http://blog.masuidrive.jp/index.php/2013/06/03/wripe-app/" target="_blank">個人でメモ帳アプリ wri.pe リリースしてみました。 - @masuidrive blog</a></td>
<td>243</td>
<td>2013/06/03</td>
</tr>
<tr>
<td><a href="http://toyoshi.hatenablog.com/entry/2013/06/15/005102" target="_blank">土日で作るWebサービス入門 - 30 to 30</a></td>
<td>1539</td>
<td>2013/06/15</td>
</tr>
<tr>
<td><a href="http://qiita.com/tumf@github/items/918ef218eeade512012c" target="_blank">Ruby - 遺伝的アルゴリズム(GA)によるサーバの自動チューニング - Qiita [キータ]</a></td>
<td>165</td>
<td>2013/06/18</td>
</tr>
<tr>
<td><a href="http://willnet.in/105" target="_blank">ランダムで日本人の名前を返す gem を作った - willnet.in</a></td>
<td>146</td>
<td>2013/07/09</td>
</tr>
<tr>
<td><a href="http://codeiq.hatenablog.com/entry/2013/07/23/104943" target="_blank">いまさらですが、増井雄一郎さんのメモ帳サービス「wri.pe」がすごい件　#HTML5 #プログラミング #wri.pe #markdown - CodeIQ Blog</a></td>
<td>838</td>
<td>2013/07/23</td>
</tr>
<tr>
<td><a href="http://shokai.org/blog/archives/8012" target="_blank">橋本商会 » ArduinoとRubyで赤外線リモコン作ってWebから操作できるようにした</a></td>
<td>140</td>
<td>2013/07/24</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/naoya/20130801/1375357430" target="_blank">HBFav2 をリリースしました - naoyaのはてなダイアリー</a></td>
<td>163</td>
<td>2013/08/01</td>
</tr>
<tr>
<td><a href="http://www.lastday.jp/2013/08/26/beginner-programmming-geekhouse-web-develop" target="_blank">プログラミング出来ないのにギークハウスを始めたら、420万円の出資を受けて1人でウェブサービスを開発することになった。 | Last Day. jp</a></td>
<td>282</td>
<td>2013/08/26</td>
</tr>
<tr>
<td><a href="http://vividcode.hatenablog.com/entry/morphana/kuromoji-cli-app" target="_blank">日本語形態素解析ライブラリ Kuromoji のコマンドライン用インターフェイスを書いた - ひだまりソケットは壊れない</a></td>
<td>222</td>
<td>2013/09/02</td>
</tr>
<tr>
<td><a href="http://anime-osusume.hatenablog.com/entry/2013/08/04/174436" target="_blank">PFI の推薦エンジンを使っておすすめアニメを探すサイトを作ってみた - アニメおすすめDB運営ブログ</a></td>
<td>131</td>
<td>2013/09/22</td>
</tr>
<tr>
<td><a href="http://itpro.nikkeibp.co.jp/article/NEWS/20130925/506807/" target="_blank">ニュース - 3社が共同開発したRuby製プロジェクト管理システム「JJ」、OSSとして無償公開へ：ITpro</a></td>
<td>173</td>
<td>2013/09/25</td>
</tr>
<tr>
<td><a href="http://anond.hatelabo.jp/20131026145638" target="_blank">ローンチしたサイトに人がこない。</a></td>
<td>362</td>
<td>2013/11/12</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/syuu1228/20131113/1384332111" target="_blank">mruby専用クラウドOS「μOSv」を作りました - 驟雨のカーネル探検隊（只今遭難中ｗ</a></td>
<td>111</td>
<td>2013/11/13</td>
</tr>
<tr>
<td><a href="http://blog.riywo.com/2013/01/07/040947" target="_blank">MyrokuというHerokuっぽいものを実装してみた - As a Futurist...</a></td>
<td>158</td>
<td>2013/01/07</td>
</tr>
</tbody>
</table>
<h3 id="opp">新しいライブラリ</h3>

昔先輩のプログラマーにこんなことを言われました。「自分が解決したい悩みがあったらまず、同じことで困っている人がいて、解法を持ってないか調べてみなさい」と。「もしそれで、解法が見つからないならばそれをライブラリーやサービスにしたらいい。ただ、ほとんどの問題はすでに誰かが壁にあったっているから、解法はすでに世の中にある」と。
ライブラリーの紹介などなど、どんなものがあるのかチェック！

<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://www.moongift.jp/2013/02/20130205/" target="_blank">社内で立てられるGistサーバ「Gistub」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td>
<td>190</td>
<td>2013/02/05</td>
</tr>
<tr>
<td><a href="http://sixeight.hatenablog.com/entry/2013/02/05/033345" target="_blank">RubyJSを試しました - ちなみに</a></td>
<td>127</td>
<td>2013/02/05</td>
</tr>
<tr>
<td><a href="http://liginc.co.jp/designer/archives/11623" target="_blank">CSSの常識が変わる！「Compass」、基礎から応用まで！ | 株式会社LIG</a></td>
<td>1188</td>
<td>2013/02/07</td>
</tr>
<tr>
<td><a href="http://el.jibun.atmarkit.co.jp/rails/2013/02/5-pythonrubytop-0220.html" target="_blank">Rails Hub情報局: 本家の5倍速？ Pythonで実装したRuby処理系の「Topaz」が登場</a></td>
<td>197</td>
<td>2013/02/07</td>
</tr>
<tr>
<td><a href="http://dev.classmethod.jp/tool/gitlab-install-mac-os-x-mountain-lion/" target="_blank">ローカルで GitHub を構築！ Git リポジトリ管理ツール「GitLab」を Mac OS X にインストールしてみた ｜ クラスメソッド開発ブログ</a></td>
<td>349</td>
<td>2013/02/07</td>
</tr>
<tr>
<td><a href="http://phpspot.org/blog/archives/2013/02/fnordmetric.html" target="_blank">どんなデータもリアルタイムなグラフにできるフレームワーク「FnordMetric」:phpspot開発日誌</a></td>
<td>103</td>
<td>2013/02/18</td>
</tr>
<tr>
<td><a href="http://blog.mirakui.com/entry/2013/02/20/003401" target="_blank">「全自動パラメータチューニングさん」は何であって何でないのか - 昼メシ物語</a></td>
<td>211</td>
<td>2013/02/20</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/bash0C7/20130313/cosmicrawler" target="_blank">Rubyで複数並行なクローラをすっきりと書けるライブラリ「cosmicrawler」をgemとして公開した - koeだめ</a></td>
<td>101</td>
<td>2013/03/13</td>
</tr>
<tr>
<td><a href="http://www.moongift.jp/2013/04/20130415/" target="_blank">iOSアプリで必要なサーバサイドの機能をまとめて提供！「Helios」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td>
<td>128</td>
<td>2013/04/15</td>
</tr>
<tr>
<td><a href="http://www.moongift.jp/2013/04/20130415-9/" target="_blank">エイプリルフールかと疑ってしまう。BashがまるでRubyのようになる「Skull」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td>
<td>128</td>
<td>2013/04/15</td>
</tr>
<tr>
<td><a href="http://www.moongift.jp/2013/04/20130428-2/" target="_blank">Rubyのコードをもっと美しく書くために使いたい「rubocop」|オープンソース・ソフトウェア、ITニュースを毎日紹介するエンジニア、デザイナー向けブログ</a></td>
<td>207</td>
<td>2013/04/28</td>
</tr>
<tr>
<td><a href="http://melborne.github.io/2013/05/20/now-the-time-to-start-jekyll/" target="_blank">Jekyllいつやるの？ジキやルの？今でしょ！</a></td>
<td>161</td>
<td>2013/05/20</td>
</tr>

<tr>
<td><a href="http://yuroyoro.hatenablog.com/entry/2013/05/29/160912" target="_blank">gfspark: GrowthForecastのグラフをターミナルに表示する - ( ꒪⌓꒪) ゆるよろ日記</a></td>
<td>104</td>
<td>2013/05/29</td>
</tr>
<tr>
<td><a href="http://gihyo.jp/dev/clip/01/groonga/0005" target="_blank">第5回　Rubyでサーバ要らずの高速全文検索！ - rroongaの紹介：隔週連載groonga｜gihyo.jp … 技術評論社</a></td>
<td>109</td>
<td>2013/06/04</td>
</tr>
<tr>
<td><a href="http://heartbeats.jp/hbblog/2013/06/use-ohai.html" target="_blank">ohaiを使ってサーバの情報をプログラムで扱おう - インフラエンジニアway - Powered by HEARTBEATS</a></td>
<td>123</td>
<td>2013/06/11</td>
</tr>
<tr>
<td><a href="http://www.atmarkit.co.jp/ait/articles/1306/14/news002.html" target="_blank">特集　DevOps時代の必須知識：まとめてたくさん処理したい！ を解決する「Capistrano」 - ＠IT</a></td>
<td>200</td>
<td>2013/07/04</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/naoya/20130912/1378963649" target="_blank">Helios - naoyaのはてなダイアリー</a></td>
<td>240</td>
<td>2013/09/12</td>
</tr>
<tr>
<td><a href="http://blog.mogya.com/2013/10/ruby-geocoder.html" target="_blank">Ruby geocoderがすごい - もぎゃろぐ</a></td>
<td>356</td>
<td>2013/10/11</td>
</tr>
<tr>
<td><a href="http://blog.glidenote.com/blog/2013/11/26/sensu/" target="_blank">監視ソフトをNagiosからSensuに切り替えて2ヶ月経ったのでまとめた - Glide Note - グライドノート</a></td>
<td>560</td>
<td>2013/11/26</td>
</tr>
<tr>
<td><a href="https://rails-assets.org/" target="_blank">Rails Assets</a></td>
<td>120</td>
<td>2013/12/13</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/dkfj/20131215/1387093204" target="_blank">Markdown記法+Git+md2review+ReVIEWで原稿・ドキュメント管理 - プログラマになりたい</a></td>
<td>111</td>
<td>2013/12/15</td>
</tr>
<tr>
<td><a href="http://takkkun.hatenablog.com/entry/2013/10/12/Capistrano_3%E3%81%B8%E3%81%AE%E6%89%8B%E5%BC%95%E3%81%8D" target="_blank">Capistrano 3への手引き - 今日のごはんは素麺です</a></td>
<td>160</td>
<td>2013/10/12</td>
</tr>
</tbody>
</table>
<h3 id="fluentd">ログ・マネージメント fluentd</h3>
今年の人気ブックマークを調べていてダントツで人気があったのが、ログ・マネージメントのライブラリfluentd。クラウドの普及によるサーバの非固定化、またデータ解析の重要性などの傾向の結果かもしれません。
<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/tagomoris/20130612/1371030356" target="_blank">ruby 2.0.0-p195 + fluentd v0.10.35 + msgpack v0.5.5 の組合せが素敵という話 - tagomorisのメモ置き場</a></td>
<td>136</td>
<td>2013/06/12</td>
</tr>
<tr>
<td><a href="http://codezine.jp/article/detail/6958" target="_blank">Fluentdで始めるリアルタイムでのログ有効活用 （1/4）：CodeZine</a></td>
<td>376</td>
<td>2013/02/14</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/dkfj/20130407/1365330503" target="_blank">何故、fluentdなのか？ - プログラマになりたい</a></td>
<td>221</td>
<td>2013/04/07</td>
</tr>
<tr>
<td><a href="http://www.slideshare.net/harukayon/fluentd-22317236" target="_blank">Fluentdがよくわからなかった話</a></td>
<td>133</td>
<td>2013/06/02</td>
</tr>
<tr>
<td><a href="http://saisa.hateblo.jp/entry/2013/08/17/182700" target="_blank">FluentdとRiakの話 - After Coding</a></td>
<td>262</td>
<td>2013/08/17</td>
</tr>
<tr>
<td><a href="http://keisukenishida.hatenablog.com/entry/2013/08/20/005026" target="_blank">fluentd で集めたログを Splunk で可視化する - 技術ノート</a></td>
<td>101</td>
<td>2013/08/20</td>
</tr>
<tr>
<td><a href="http://jedipunkz.github.io/blog/2013/09/07/kibana-plus-elasticsearch-plus-fluentd/" target="_blank">Kibana + ElasticSearch + fluentd を試してみた - jedipunkz' blog</a></td>
<td>100</td>
<td>2013/09/07</td>
</tr>
<tr>
<td><a href="http://y310.hatenablog.com/entry/2013/09/11/232137" target="_blank">Kibana 3 + Rails + Fluentdのサンプルアプリを作ってみた - y_310's diary</a></td>
<td>170</td>
<td>2013/09/12</td>
</tr>
<tr>
<td><a href="http://techblog.raccoon.ne.jp/archives/35031163.html" target="_blank">fluentd(td-agent) の導入 : Raccoon Tech Blog [株式会社ラクーン 技術戦略部ブログ]</a></td>
<td>105</td>
<td>2013/12/02</td>
</tr>
<tr>
<td><a href="http://tagomoris.hatenablog.com/entry/2013/12/03/150656" target="_blank">Fluentdとはどのようなソフトウェアなのか - たごもりすメモ</a></td>
<td>565</td>
<td>2013/12/03</td>
</tr>
<tr>
<td><a href="http://knowledge.sakura.ad.jp/tech/1336/" target="_blank">柔軟なログ収集を可能にする「fluentd」入門 - さくらのナレッジ</a></td>
<td>301</td>
<td>2013/12/09</td>
</tr>
</tbody>
</table>
<h3 id="tips">Tips! コーディング</h3>
まとめきれなかったけど、人気のあるTips、コーディングについての記事です。
<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://melborne.github.com/2013/03/04/ruby-trivias-you-should-know-4/" target="_blank">知って得する！５５のRubyのトリビアな記法</a></td>
<td>632</td>
<td>2013/03/04</td>
</tr>
<tr>
<td><a href="http://shokai.org/blog/archives/7262" target="_blank">橋本商会 » Ruby書くならBundler使え</a></td>
<td>159</td>
<td>2013/03/29</td>
</tr>
<tr>
<td><a href="http://blog.livedoor.jp/sasata299/archives/51889303.html" target="_blank">Redisでランキング機能を実装してみる - (ﾟ∀ﾟ)o彡 sasata299's blog</a></td>
<td>121</td>
<td>2013/04/24</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/naoya/20130503/1367581629" target="_blank">昨今の自分用Webアプリケーションひな形 - naoyaのはてなダイアリー</a></td>
<td>514</td>
<td>2013/05/03</td>
</tr>
<tr>
<td><a href="http://melborne.github.io/2011/06/22/21-Ruby-21-Trivia-Notations-you-should-know-in-Ruby/" target="_blank">知って得する21のRubyのトリビアな記法</a></td>
<td>106</td>
<td>2013/05/10</td>
</tr>
<tr>
<td><a href="http://techracho.bpsinc.jp/morimorihoge/2013_05_16/8664" target="_blank">RubyでExcelデータをJSON形式に変換するには | TechRacho</a></td>
<td>109</td>
<td>2013/05/16</td>
</tr>
<tr>
<td><a href="http://tech.a-listers.jp/2013/05/20/sandi-metz/" target="_blank">綺麗な設計を身に付けるためのSandi Metzルール | A-Listers</a></td>
<td>199</td>
<td>2013/05/20</td>
</tr>
<tr>
<td><a href="http://qiita.com/camelmasa/items/5ca27ab398f105f86c76" target="_blank">Ruby - Bundlerで並列処理？？bundle installを爆速で処理する方法。 - Qiita [キータ]</a></td>
<td>158</td>
<td>2013/08/10</td>
</tr>
<tr>
<td><a href="http://melborne.github.io/2013/09/04/is-that-a-yet-another-rdoc/" target="_blank">メソッドの使い方もRubyに教えてほしい</a></td>
<td>111</td>
<td>2013/09/04</td>
</tr>
<tr>
<td><a href="http://makimoto.hatenablog.com/entry/2013/10/20/Ruby_Hacking_Guide_%E3%82%92_Kindle_%E3%81%A7%E8%AA%AD%E3%82%81%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%99%E3%82%8B" target="_blank">Ruby Hacking Guide を Kindle で読めるようにする - Stats of the Rivers</a></td>
<td>189</td>
<td>2013/10/20</td>
</tr>
<tr>
<td><a href="http://qiita.com/jnchito/items/dedb3b889ab226933ccf" target="_blank">[初心者向け] RubyやRailsでリファクタリングに使えそうなイディオムとか便利メソッドとか - Qiita [キータ]</a></td>
<td>286</td>
<td>2013/11/05</td>
</tr>
<tr>
<td><a href="http://www.find-job.net/startup/english-for-engineers-naming-conventions" target="_blank">正しいコーディングが身につくエンジニア英語の手引き 〜文法とクラス／メソッド、命名規則〜 | Find Job ! Startup</a></td>
<td>1140</td>
<td>2013/11/05</td>
</tr>
<tr>
<td><a href="https://speakerdeck.com/tmtms/ben-dang-hakowaienkodeingufalsehua" target="_blank">本当はこわいエンコーディングの話 // Speaker Deck</a></td>
<td>197</td>
<td>2013/01/13</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/maeharin/20130118/php_ruby_love" target="_blank">PHPを愛する試み - maeharinの日記</a></td>
<td>190</td>
<td>2013/01/18</td>
</tr>
<tr>
<td><a href="http://melborne.github.com/2013/01/24/csv-table-method-is-awesome/" target="_blank">Ruby標準添付ライブラリcsvのCSV.tableメソッドが最強な件について</a></td>
<td>146</td>
<td>2013/01/24</td>
</tr>
<tr>
<td><a href="http://www.slideshare.net/shokai/ruby-24925828" target="_blank">Ruby中級入門</a></td>
<td>541</td>
<td>2013/08/05</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/shim0mura/20130117/1358436466" target="_blank">読みやすいコードってどんなものか考えてみた -抽象化と名前重要- - 馬鹿と天才は紙一重</a></td>
<td>517</td>
<td>2013/01/18</td>
</tr>
<tr>
<td><a href="http://nekogata.hatenablog.com/entry/2013/02/09/233540" target="_blank">"状態管理用の変数をインスタンスに持たせるなこのタコって話 - life.should be_happy # =&gt; 1 examples</a></td>
<td>? failures"</td>
<td>399,2013/02/09</td>
</tr>
<tr>
<td><a href="http://melborne.github.com/2013/02/25/i-wanna-say-something-about-rubys-case/" target="_blank">Rubyのcaseを〇〇(言語名)のswitch文だと思っている人たちにぼくから一言ガツンと申し上げたい</a></td>
<td>516</td>
<td>2013/02/25</td>
</tr>
<tr>
<td><a href="http://d.hatena.ne.jp/authorNari/20130120/1358676294" target="_blank">SPDYと「やったー、net-http-spdyできたよー」の話 - I am Cruby!</a></td>
<td>139</td>
<td>2013/01/20</td>
</tr>
</tbody>
</table>

<h3 id="clientbackend">クライアントサイドとバックエンド</h3>

Backborn.js, Ember.js, Angular.js, Meteorなど、たくさんのクライアントサイドJavascript Frameworkがでて、人気を集めています。RubyやRailsのプログラマはそれをどのように捉えているのでしょうか。バックエンドについての記事と一緒に紹介します。

<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://wazanova.jp/post/64057743910/mvc-gogaruco-2013" target="_blank">ダブルMVCの意味するところ [GoGaRuCo 2013] - ワザノバ | wazanova.jp</a></td>
<td>130</td>
<td>2013/10/15</td>
</tr>
<tr>
<td><a href="https://gist.github.com/tily/1362110" target="_blank">サバクラ両方で動く JavaScript の大規模開発を行うために</a></td>
<td>368</td>
<td>2013/02/09</td>
</tr>
<tr>
<td><a href="http://dev.classmethod.jp/client-side/language-client-side/backbonejs-mvp/" target="_blank">Backbone.jsにおけるModel-View-Presenterアーキテクチャパターン ｜ クラスメソッド開発ブログ</a></td>
<td>162</td>
<td>2013/02/26</td>
</tr>
<tr>
<td><a href="http://blog.riywo.com/2013/05/29/151321" target="_blank">「これからのWeb(バックエンド)」を自分の頭で考えてみた - As a Futurist...</a></td>
<td>256</td>
<td>2013/05/29</td>
</tr>
</tbody>
</table>

<h3 id="env">Rubyを取り巻く環境、組織</h3>
Rubyを取り巻く環境について、イノベーション、OSS、他の言語やモバイル。そして働く組織の話も多くのブックマークを集めました。
<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr>
<td><a href="http://engineer.typemag.jp/article/matzxmasuidrive" target="_blank">まつもとゆきひろ×増井雄一郎のオープンソース談義 「1人の熱烈なフォロワーがいれば、OSSで世界を変えられる」 - エンジニアtype</a></td>
<td>168</td>
<td>2013/03/25</td>
</tr>
<tr>
<td><a href="http://www.atmarkit.co.jp/ait/articles/1304/16/news133.html" target="_blank">日本はもっと、エンジニアを大切に：まつもとゆきひろ氏の「新経済サミット2013」語録 - ＠IT</a></td>
<td>264</td>
<td>2013/04/16</td>
</tr>
<tr>
<td><a href="http://internet.watch.impress.co.jp/docs/event/20130417_596169.html" target="_blank">LINE、グリー、GMOのトップが激論――日本でイノベーションを起こすには？ -INTERNET Watch</a></td>
<td>144</td>
<td>2013/04/17</td>
</tr>
<tr>
<td><a href="http://tadachi.txt-nifty.com/blog/2013/05/post-176e.html" target="_blank">まつもとゆきひろ氏の「世界に通用する技術者になるためには」を聴講してきた: tadachi-net 出張所</a></td>
<td>251</td>
<td>2013/05/19</td>
</tr>
<tr>
<td><a href="http://eed3si9n.com/ja/simplicity-matters" target="_blank">シンプルさの必要性 | eed3si9n</a></td>
<td>146</td>
<td>2013/06/24</td>
</tr>
<tr>
<td><a href="https://speakerdeck.com/kuromatu/rubykaraphphe-enziniafalsetamefalsesi-kao-yi-xing-gaido" target="_blank">RubyからPHPへ -エンジニアのための思考移行ガイド- // Speaker Deck</a></td>
<td>103</td>
<td>2013/09/14</td>
</tr>
<tr>
<td><a href="http://ds.freee.co.jp/2013/11/18/google/" target="_blank">僕が Google を辞めた理由 | クラウド会計ソフト freee - 佐々木大輔のブログ</a></td>
<td>467</td>
<td>2013/11/18</td>
</tr>
<tr>
<td><a href="http://internet.watch.impress.co.jp/docs/news/20131203_626035.html" target="_blank">まつもとゆきひろ氏「プログラミングコミュニティーは終わらない文化祭」 -INTERNET Watch</a></td>
<td>177</td>
<td>2013/12/03</td>
</tr>
<tr>
<td><a href="http://www.publickey1.jp/blog/13/sfdc2013.html" target="_blank">PR：伊藤直也×まつもとゆきひろ。ポストPC時代のモバイル開発を語る － Publickey</a></td>
<td>190</td>
<td>2013/08/26</td>
</tr>
<tr>
<td><a href="https://speakerdeck.com/robotvert/about-cookpad-2013-11" target="_blank">About COOKPAD (2013-11) // Speaker Deck</a></td>
<td>143</td>
<td>2013/11/19</td>
</tr>
<tr>
<td><a href="http://wazanova.jp/items/675" target="_blank">Githubの組織が成長する過程で変えたことと変えなかったこと - ワザノバ | wazanova</a></td>
<td>638</td>
<td>2013/11/20</td>
</tr>
</tbody>
</table>


<h3 id="func">TwitterがRubyからJVM 言語群へ。関数型言語のトレンド</h3>

最後にTwitterがRubyからJVM 言語群への移行をおこなった（おこなっている）。また、クロック数の限界とCPUコア数の増加から、関数型言語への注目が集まりました。これからのRubyやプログラミングについて考えるのにいいトピックだとおもい、このトピックで今年2013年の話題の振り返りを終わりにします。

<table>
<tbody>
<tr>
<th>記事</th>
<th>users数</th>
<th>登録日</th>
</tr>
<tr><td><a href="http://2013.8-p.info/japanese/09-28-languages.html" target='_blank'>はじめの言語の賞味期限 - Kato Kazuyoshi</a></td><td>359</td><td>2013/09/28</td></tr>
<tr><td><a href="http://blog.livedoor.jp/itsoku/archives/33671593.html" target='_blank'>GitHubがRubyとMVCの限界を悟り、C#とMVVMに全面移行！！ : IT速報</a></td><td>167</td><td>2013/10/05</td></tr>
<tr><td><a href="http://www.find-job.net/startup/architecture-2013" target='_blank'>国内注目のWebサービスを支える言語・フレームワーク・アーキテクチャ一覧【2013年版】 | Find Job ! Startup</a></td><td>1169</td><td>2013/10/17</td></tr>
<tr><td><a href="http://wazanova.jp/post/66950939518/twitter" target='_blank'>Twitter: 大きなトラフィックに耐えうるアーキテクチャーへの変更 - ワザノバ | wazanova.jp</a></td><td>119</td><td>2013/11/14</td></tr>
<tr><td><a href="http://www.infoq.com/jp/news/2013/08/scaling-twitter" target='_blank'>Twitterのスケーリング，新たなピークへ</a></td><td>258</td><td>2013/08/29</td></tr>
<tr><td><a href="http://d.hatena.ne.jp/camlspotter/20130117/1358406799" target='_blank'>"関数型言語を独学で勉強している学生です への答 - Oh</a></td><td> you `re no (fun _ → more)"</td><td>118,2013/01/17</td></tr>
<tr><td><a href="http://melborne.github.com/2013/01/21/why-fp-with-ruby/" target='_blank'>Rubyを使って「なぜ関数プログラミングは重要か」を読み解く（改定）─ 前編 ─ 但し後編の予定なし</a></td><td>186</td><td>2013/01/21</td></tr>
<tr><td><a href="http://www.h6.dion.ne.jp/~machan/misc/FPwithRuby.html" target='_blank'>Rubyによる関数型プログラミング</a></td><td>295</td><td>2013/02/03</td></tr>
<tr><td><a href="http://itpro.nikkeibp.co.jp/article/COLUMN/20130112/449223/" target='_blank'>Javaはもう古い！次の主流は「関数型」 - ［関数型言語のトレンド］国内でも採用企業が増加：ITpro</a></td><td>270</td><td>2013/02/04</td></tr>
<tr><td><a href="http://yuroyoro.hatenablog.com/entry/2013/03/27/190640" target='_blank'>Rubyで関数合成とかしたいので lambda_driver.gem というのを作った - ( ꒪⌓꒪) ゆるよろ日記</a></td><td>166</td><td>2013/03/27</td></tr>
</tbody>
</table>


2013年人気のあった記事を話題別にまとめてみました。トレンドや見逃していた記事、やり残したことが見つかると幸いです。
