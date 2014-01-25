---
layout: post
status: publish
published: true
title: 2013年Chefの話題を一挙に振り返るまとめ
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 2104
wordpress_url: http://www.engineyard.co.jp/blog/?p=2104
date: 2013-12-18 13:55:24.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/iStock_000020118226XSmall.jpg" alt="iStock_000020118226XSmall" width="425" height="282" class="alignnone size-full wp-image-2117" />
早いもので2013年もまもなく終わります。特にChefについては今年は大きな飛躍の1年になりました。Chefについては話題の流れも多く、自身としても何があったのかを即座には思い出せません。今回はすでにChefを使っている人の話題の復習や、Chefをまだキャッチアップしていない人が今からでも間に合う情報収集としてまとめてみます。

はてなブックマーク上でも2013年の記事でChefタグが付けられた3ブックマーク以上の記事が<strong>800エントリを超え、ブックマークの回数は3万2千回を超えるというとてつもない状況です</strong>。今回はその中でも100ブックマーク以上が付いた記事の中から特に注目が集まった話題を時系列で振り返ります。

<h3>2013年1月:「兆し」</h3>
2013年早々にChefの大躍進の契機になるエントリが@naoya_itoさんのブログに投稿されます。「開発メモ#4 : EC2スナップショットとの差分は chef-solo で解決」と題されたエントリでchef-soloを使ってEC2のスナップショットに新しいIPアドレスを反映するというような流れが紹介されています。今の時点ので考えるとこれはプロビジョニングというよりもオーケストレーションのような部分に近く、ソフトウェアのインストールなどではなく動作環境に適切な情報を埋め込む為の利用用途になっています。

ただすでにこの時点でツールチェインとしてレシピに対するテストを実行する事が示唆されています。

<blockquote>
<ul>
				<li> ローカルでレシピ (chef) をがりがり書く</li>
				<li> chef レシピの lint <a href="http://acrmp.github.com/foodcritic/">foodcritic</a> でチェック</li>
				<li> git commit して github に push</li>
				<li> chef-solo を Cinnamon を使って、リモートで実行</li>
				<li> リモートでは git fetch で最新のレシピを取ってきて、chef-solo が実行される</li>
</ul>
</blockquote>

foodcriticは実際にクックブックを動作させるのではなく、シンタックスベースでのテストを行いますがすでにテストの必要性が提起されています。またこのエントリ内でも言及されていますが、@sawanobolyさんによる「Cucumber, ChefSpecとchefでテスト駆動のサーバ構築管理」と題されたエントリが公開されておりサーバーの構成を継続的にテストする手法が提示されています。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://blog.riywo.com/2013/01/07/040947' target='_blank'>MyrokuというHerokuっぽいものを実装してみた - As a Futurist...</a></td><td>158</td><td>2013/01/07</td></tr>
<tr><td><a href='http://heartbeats.jp/hbblog/2013/01/chef-cookbook-tips.html' target='_blank'>ChefでCookbookを作成するときのちょっとしたコツ 9選 - インフラエンジニアway - powered by HEARTBEATS</a></td><td>186</td><td>2013/01/23</td></tr>
<tr><td><a href='http://qiita.com/sawanoboly/items/48fe830d2ee3b6c87bf5' target='_blank'><strong>Cucumber, ChefSpecとchefでテスト駆動のサーバ構築管理 #infrastructure #Cucumber #Ruby #chef #chefspec - Qiita</strong></a></td><td>120</td><td>2013/01/27</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130131/1359614077' target='_blank'><strong>開発メモ#4 : EC2スナップショットとの差分は chef-solo で解決 - naoyaのはてなダイアリー</strong></a></td><td>139</td><td>2013/01/31</td></tr>
</table>

<h3>2013年2月:「勉強会、AWS OpsWorksの発表」</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/02/859294_277535169044078_1639743555_o.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/02/859294_277535169044078_1639743555_o-1024x768.jpg" alt="859294_277535169044078_1639743555_o" width="1024" height="768" class="alignnone size-large wp-image-603" /></a>

2月はEngine Yardで開催した「初めてのChefの教室」でのコンテンツなどに注目が集まり、方法論の交流が活発になりました。またFacebookでの大規模な採用事例やその知見を反映したChef11が公開されました。
Chefとセットで使われる事の多いツール、Vagrantが@naoya_itoさんのブログで紹介され事実上Chefを使う際の必須ツールになったのも2月の出来事でした。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130204/1359971408' target='_blank'>開発メモ#5 : Amazon Linux で knife-solo を使って chef-solo 実行 - naoyaのはてなダイアリー</a></td><td>107</td><td>2013/02/04</td></tr>
<tr><td><a href='http://www.publickey1.jp/blog/13/facebookchefcheferlangopscode.html' target='_blank'>Facebook、データセンター自動化ツールにChefの新バージョンを全面採用、Erlangでスケーラビリティ拡大。OpsCodeが発表 － Publickey</a></td><td>167</td><td>2013/02/05</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130205/1360062070' target='_blank'><strong>Vagrant - naoyaのはてなダイアリー</strong></a></td><td>962</td><td>2013/02/05</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130205/1360088927' target='_blank'>LTSVフォーマットなログを fluentd + GrowthForecast で料理 - naoyaのはてなダイアリー</a></td><td>266</td><td>2013/02/06</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130207/1360240992' target='_blank'>【今北産業】3分で分かるLTSV業界のまとめ【LTSV】 - naoyaのはてなダイアリー</a></td><td>328</td><td>2013/02/07</td></tr>
<tr><td><a href='https://speakerdeck.com/mirakui/quan-zi-dong-parametatiyuningusan' target='_blank'>全自動パラメータチューニングさん // Speaker Deck</a></td><td>353</td><td>2013/02/18</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130219/1361262854' target='_blank'>開発メモ#6 : ログの取り扱い : GrowthForecast, Amazon S3, Treasure Data で心労ゼロ - naoyaのはてなダイアリー</a></td><td>244</td><td>2013/02/19</td></tr>
<tr><td><a href='http://aws.typepad.com/aws_japan/2013/02/aws-opsworks-flexible-application-management-in-the-cloud.html' target='_blank'>Amazon Web Services ブログ: 【AWS発表】AWS OpsWorks - Chefを使って柔軟にクラウド内のアプリケーション管理ができる新サービスを発表</a></td><td>332</td><td>2013/02/19</td></tr>
<tr><td><a href='http://www.publickey1.jp/blog/13/amazonaws_opsworkschef.html' target='_blank'>Amazonクラウド、デプロイの自動化ツール「AWS OpsWorks」公開。Chefのレシピ利用 － Publickey</a></td><td>109</td><td>2013/02/20</td></tr>
<tr><td><a href='http://www.engineyard.co.jp/blog/2013/engineyard-meetup-chef-seminar/' target='_blank'><strong>「初めてのChefの教室」を開催しました。(動画&資料) - Engine Yard Blog JP</strong></a></td><td>399</td><td>2013/02/25</td></tr>
<tr><td><a href='http://www.akiyan.com/blog/archives/2013/02/chef-is-the-technology-in-which-study-cost-performance-is-the-highest-now.html' target='_blank'>今もっとも学習コスパの高い技術はChefだと、Chef勉強会に行って確信した - akiyan.com</a></td><td>599</td><td>2013/02/25</td></tr>
<tr><td><a href='http://dann.g.hatena.ne.jp/dann/20130225/p1' target='_blank'>ChefでMacを開発マシンとしてセットアップ - dann's blog - #</a></td><td>219</td><td>2013/02/25</td></tr>
<tr><td><a href='http://www.ryuzee.com/contents/blog/6371' target='_blank'>ChefのrecipeをJenkinsで継続的インテグレーションする方法 | Ryuzee.com</a></td><td>119</td><td>2013/02/27</td></tr>
</table>

<h3>2013年3月: 「入門 Chef Soloとserverspecの登場」</h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/Kindle向けに『入門Chef_Solo_-_Infrastructure_as_Code』を出版しました_-_naoyaのはてなダイアリー.png" alt="Kindle向けに『入門Chef_Solo_-_Infrastructure_as_Code』を出版しました_-_naoyaのはてなダイアリー" width="821" height="356" class="alignnone size-full wp-image-2128" />

3月の出来事はなんといっても電子書籍「入門Chef Solo」の出版が大きいです。KDP上での出版という動きの中でもかなり早期のものでランキング上位に今でも入っています。一方で「Chefに挫折した」という層も出始めたのかFabricについての記事にも注目が集まりました。現在でも話題になっているserverspecに注目が集まったのも3月の出来事です。

Chefが中心の記事ではないですが「同僚の外国人プログラマ観察記録」はVagrantやBerkshelf、SublimeText2、NewRelicなどを使って楽をしていた外国人プログラマの姿が紹介されています。この時点ではある種「未来的なプログラマ像」のように描かれていたように思いますが、同じようなスタイルを取っている人は増えてきているかもしれません。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://d.hatena.ne.jp/int128/20130302/1362153651' target='_blank'>GitとJenkinsを使ってChefを運用する - GeekFactory</a></td><td>265</td><td>2013/03/02</td></tr>
<tr><td><a href='http://www.slideshare.net/YukihikoSawanobori/what-is-chef201303' target='_blank'>What is chef</a></td><td>257</td><td>2013/03/04</td></tr>
<tr><td><a href='http://tk0miya.hatenablog.com/entry/2013/03/07/121438' target='_blank'>開発サーバに chef を入れるときの 11個の方法 - Hack like a rolling stone</a></td><td>233</td><td>2013/03/07</td></tr>
<tr><td><a href='http://hozumi.github.com/2013/03/chef-fabric-ja.html' target='_blank'><strong>Chefに挫折したあなたへ。Fabricのすすめ</strong></a></td><td>232</td><td>2013/03/11</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130313/1363129532' target='_blank'><strong>Kindle向けに『入門Chef Solo - Infrastructure as Code』を出版しました - naoyaのはてなダイアリー</strong></a></td><td>347</td><td>2013/03/13</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130315/1363340698' target='_blank'>Vagrant 1.1 で EC2 を vagrant up - naoyaのはてなダイアリー</a></td><td>195</td><td>2013/03/15</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/dkfj/20130317/1363485034' target='_blank'>手動でサーバの設定をすることを禁ずる。入門Chef Solo - プログラマになりたい</a></td><td>213</td><td>2013/03/17</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/masudaK/20130320/1363794789' target='_blank'>Chefのテストスイーツを色々試してみた （1） - カイワレの大冒険</a></td><td>145</td><td>2013/03/21</td></tr>
<tr><td><a href='http://banyan.github.com/2013/03/21/1/' target='_blank'>社内で Chef 勉強会をして色々教えてもらった - banyan.github.com</a></td><td>120</td><td>2013/03/21</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130321/1363838408' target='_blank'>宮川さんPodcast ep6、KDP での本の作り方 - naoyaのはてなダイアリー</a></td><td>142</td><td>2013/03/21</td></tr>
<tr><td><a href='http://www.1x1.jp/blog/2013/03/vagrant.html' target='_blank'>こりゃ便利！Vagrant で自分の PC に「作って、壊して、元に戻せる」サーバを作る - Shin x blog</a></td><td>577</td><td>2013/03/22</td></tr>
<tr><td><a href='http://tatsu-zine.com/books/chef-solo' target='_blank'>入門Chef Solo - Infrastructure as Code - 達人出版会</a></td><td>191</td><td>2013/03/22</td></tr>
<tr><td><a href='http://tsuchikazu.net/chef_solo_start/' target='_blank'>Chef Soloの正しい始め方 | tsuchikazu blog</a></td><td>158</td><td>2013/03/23</td></tr>
<tr><td><a href='http://rinu.hatenablog.com/entry/2013/03/17/164151' target='_blank'><strong>同僚の外国人プログラマ観察記録 - rinu's blog</strong></a></td><td>1766</td><td>2013/03/23</td></tr>
<tr><td><a href='http://mizzy.org/blog/2013/03/23/1/' target='_blank'>Puppet や Chef で構築したサーバを RSpec でテストする - Gosuke Miyashita</a></td><td>169</td><td>2013/03/23</td></tr>
<tr><td><a href='http://mizzy.org/blog/2013/03/24/3/' target='_blank'>構築済みサーバを RSpec でテストする serverspec という gem をつくった - Gosuke Miyashita</a></td><td>210</td><td>2013/03/24</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/ntaku/20130324/1364132658' target='_blank'>入門Chef-Soloを片手にRailsアプリを動作させるところまでやってみた - プログラミングノート</a></td><td>119</td><td>2013/03/24</td></tr>
<tr><td><a href='http://heartbeats.jp/hbblog/2013/03/chef-recipe-and-lib.html' target='_blank'>「写経」から始めるChefクックブックの作成 - インフラエンジニアway - Powered by HEARTBEATS</a></td><td>284</td><td>2013/03/27</td></tr>
<tr><td><a href='http://serverspec.org/' target='_blank'><strong>serverspec - home</strong></a></td><td>139</td><td>2013/03/30</td></tr>
</table>

<h3>2013年4月: 「研修での採用事例とAnsible」</h3>
4月ということで研修の一環としてChefなどを使う事例が紹介されるようになります。サーバーの設定作業をChefなどを使って行うのが当たり前というエンジニアが続々と誕生していったという事でこれは後に繋がりそうです。またChefに馴染みにくかった方の中でAnsibleやFabricなどの同種のツールの活用も紹介されています。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://d.hatena.ne.jp/dkfj/20130404/1365048462' target='_blank'>運用視点でChef ServerかChef Solo + Knife Soloのどちらが良いか考えてみた - プログラマになりたい</a></td><td>135</td><td>2013/04/04</td></tr>
<tr><td><a href='https://gist.github.com/hsbt/5316074' target='_blank'><strong>2013 年の新卒研修メニュー - gist:5316074</strong></a></td><td>108</td><td>2013/04/05</td></tr>
<tr><td><a href='http://apatheia.info/blog/2013/04/06/about-ansible/' target='_blank'><strong>構成管理ツール Ansible について - apatheia.info</strong></a></td><td>254</td><td>2013/04/07</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/dkfj/20130407/1365330503' target='_blank'>何故、fluentdなのか？ - プログラマになりたい</a></td><td>220</td><td>2013/04/07</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/thinkAmi/20130407/1365310673' target='_blank'>Windows7上で Vagrant + Chef solo + knife-soloを使い、Ubuntu + ubuntu-desktopの環境を構築してみた - メモ的な思考的な</a></td><td>145</td><td>2013/04/07</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/shiumachi/20130414/1365920515' target='_blank'>今日からすぐに使えるデプロイ・システム管理ツール Fabric 入門 - 科学と非科学の迷宮</a></td><td>360</td><td>2013/04/14</td></tr>
<tr><td><a href='http://tech.kayac.com/archive/2013training.html' target='_blank'><strong>2013年の新卒研修と社内ISUCONやりました - (1) 研修編 | tech.kayac.com - KAYAC engineers' blog</strong></a></td><td>246</td><td>2013/04/22</td></tr>
<tr><td><a href='http://steps.dodgson.org/b/2013/04/24/recent-happenings-on-elders/' target='_blank'>最近のおっさんたち - steps to phantasien</a></td><td>291</td><td>2013/04/24</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/dkfj/20130425/1366852899' target='_blank'>サーバ構築・デプロイの自動化の話。或いはChefとCapistranoの素敵な関係 - プログラマになりたい</a></td><td>111</td><td>2013/04/25</td></tr>
<tr><td><a href='http://blog.kentarok.org/entry/2013/04/30/225404' target='_blank'>『入門Puppet - Automate Your Infrastructure』という電子書籍を出版しました - delirious thoughts</a></td><td>182</td><td>2013/04/30</td></tr>
</table>

<h3>2013年5月: 「serverspecを使ったCIが定着」</h3>
5月の時点ではこれまでに話題になってきた技術の組み合わせが普及する時期だったようです。さまざまな場面でserverspecとChefを組み合わせた事例が紹介されており、ChefSpecなどを使ってテストを行うという人よりもserverspecから始める人が主流になっていったようです。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://takatoshimaeda.github.io/blog/2013/05/07/create-server-30-minutes/' target='_blank'>[Chef][serverspec]ChefSoloを使ってnginx+mysql+rubyサーバー(VPS)を30分で作る - takatoshi blog</a></td><td>129</td><td>2013/05/07</td></tr>
<tr><td><a href='https://speakerdeck.com/naoya/ru-men-chef-sololuo-tisui-shi-i' target='_blank'>入門Chef Solo落ち穂拾い // Speaker Deck</a></td><td>188</td><td>2013/05/10</td></tr>
<tr><td><a href='http://blog.inouetakuya.info/entry/20130511/1368271417' target='_blank'><strong>Chef と Puppet の勉強会というよりも、むしろ時代は serverspec だった #pfcasual - 彼女からは、おいちゃんと呼ばれています</strong></a></td><td>314</td><td>2013/05/11</td></tr>
<tr><td><a href='http://dev.classmethod.jp/news/lesson8-done/' target='_blank'>【勉強会】AWS管理を自動化する奥義を開催しました！ ｜ Developers.IO</a></td><td>116</td><td>2013/05/16</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130520/1369054828' target='_blank'><strong>Vagrant + Chef Solo + serverspec + Jenkins でサーバー構築を CI - naoyaのはてなダイアリー</strong></a></td><td>427</td><td>2013/05/20</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130521/1369102714' target='_blank'>Vagrant + Jenkins の CI を AWS でも回す - naoyaのはてなダイアリー</a></td><td>174</td><td>2013/05/21</td></tr>
<tr><td><a href='http://tk0miya.hatenablog.com/entry/2013/05/24/153325' target='_blank'>chef で mysql のユーザやデータベースを管理する - Hack like a rolling stone</a></td><td>127</td><td>2013/05/24</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/rx7/20130526/p1' target='_blank'>Chef 11 での client/server/knife のセットアップ手順(+α) - 元RX-7乗りの適当な日々</a></td><td>186</td><td>2013/05/27</td></tr>
<tr><td><a href='http://qiita.com/tumf/items/bb90e266016e0dc85c4e' target='_blank'>CentOSの要らないサービスを無効にするレシピ - Qiita [キータ]</a></td><td>102</td><td>2013/05/29</td></tr>
<tr><td><a href='http://blog.riywo.com/2013/05/29/151321' target='_blank'>「これからのWeb(バックエンド)」を自分の頭で考えてみた - As a Futurist...</a></td><td>256</td><td>2013/05/29</td></tr>
</table>

<h3>2013年6月:「VPSでの事例とDocker」</h3>
引き続き利用が拡大し、AWSやVirtualBox以外の環境での利用例が話題になっています。また最近の話題をさらっているDockerが@naoya_itoさんによって紹介されています。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://www.slideshare.net/cloned/php-kansai2013-lt' target='_blank'>一人でゲームをリリースするための自動化 PHPUnit編 ~目指せCoverage 100%~</a></td><td>102</td><td>2013/06/02</td></tr>
<tr><td><a href='http://orangain.hatenablog.com/entry/multi-node-serves-using-lxc-on-sakura-vps' target='_blank'>さくらVPSでLXCを使って安価に複数台構成を実現する - orangain flavor</a></td><td>437</td><td>2013/06/06</td></tr>
<tr><td><a href='http://heartbeats.jp/hbblog/2013/06/use-ohai.html' target='_blank'>ohaiを使ってサーバの情報をプログラムで扱おう - インフラエンジニアway - Powered by HEARTBEATS</a></td><td>122</td><td>2013/06/11</td></tr>
<tr><td><a href='http://qiita.com/tumf@github/items/918ef218eeade512012c' target='_blank'>Ruby - 遺伝的アルゴリズム(GA)によるサーバの自動チューニング - Qiita [キータ]</a></td><td>165</td><td>2013/06/18</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20130620/1371729625' target='_blank'><strong>Docker (土曜日に podcast します) - naoyaのはてなダイアリー</strong></a></td><td>105</td><td>2013/06/20</td></tr>
<tr><td><a href='http://www.slideshare.net/AmazonWebServicesJapan/20130506-23096544' target='_blank'>AWS上でのWebアプリケーションデプロイ</a></td><td>353</td><td>2013/06/21</td></tr>
<tr><td><a href='https://speakerdeck.com/tnmt/puppet-and-chef' target='_blank'>Puppet & Chef // Speaker Deck</a></td><td>140</td><td>2013/06/21</td></tr>
<tr><td><a href='http://www.slideshare.net/mizzy/serverspec-hbstudy45' target='_blank'>Serverspec at hbstudy #45</a></td><td>137</td><td>2013/06/22</td></tr>
<tr><td><a href='http://www.ryuzee.com/contents/blog/6690' target='_blank'>ChefのCookbookのベストプラクティス | Ryuzee.com</a></td><td>108</td><td>2013/06/22</td></tr>
<tr><td><a href='http://www.creationline.com/lab/3080' target='_blank'>[和訳] 初心者Chefアンチパターン by Julian Dunn #opschef_ja « CREATIONLINE, INC.</a></td><td>166</td><td>2013/06/25</td></tr>
</table>

<hr/>
Engine Yard CloudはAWSやWindows Azureなどのクラウド環境をChefで構築するPaaSです。有人運用などをサポートで提供しています。
<a href="http://ey.io/noyakshave"><img src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png"></a>
<hr/>

<h3>2013年7月: 「メディアへの露出」</h3>
<a href="http://www.flickr.com/photos/yandod/9302868729/" title="Untitled by yandod, on Flickr"><img src="http://farm4.staticflickr.com/3771/9302868729_56cd0a01ca_c.jpg" width="800" height="534" alt="Untitled"></a>

7月にはVagrantの作者のMitchell Hashimotoさんが来日し講演した事がメディアにも掲載されました。DevOpsの流れの中でChefはツールセットの中の一部として定着し引き続き注目されています。またPHPカンファレンス関西での紹介がきっかけにPHPの開発にVagrantを使うという話題が出始めたころでもあります。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://www.atmarkit.co.jp/ait/articles/1307/02/news002.html' target='_blank'>特集　DevOps時代の必須知識：いまさら聞けない「DevOps」 (1/2) - ＠IT</a></td><td>160</td><td>2013/07/02</td></tr>
<tr><td><a href='http://www.atmarkit.co.jp/ait/articles/1305/24/news003.html' target='_blank'>特集　DevOps時代の必須知識：インフラストラクチャ自動化フレームワーク「Chef」の基本 (1/2) - ＠IT</a></td><td>329</td><td>2013/07/03</td></tr>
<tr><td><a href='http://dev.classmethod.jp/tool/vagrant/' target='_blank'>Vagrantを使って仮想OSを簡単に作成しよう ｜ Developers.IO</a></td><td>104</td><td>2013/07/03</td></tr>
<tr><td><a href='http://www.atmarkit.co.jp/ait/articles/1306/14/news002.html' target='_blank'>特集　DevOps時代の必須知識：まとめてたくさん処理したい！ を解決する「Capistrano」 - ＠IT</a></td><td>200</td><td>2013/07/04</td></tr>
<tr><td><a href='http://www.engineyard.co.jp/blog/2013/chef-tutorial-updated/' target='_blank'><strong>「初めてのChefの教室」をアップデートしました | Engine Yard Blog JP</strong></a></td><td>185</td><td>2013/07/06</td></tr>
<tr><td><a href='http://developer.smartnews.be/blog/2013/07/08/cloud-service-management-using-chef-and-fabric/' target='_blank'>chef + fabricを用いたクラウドサービス管理 | SmartNews開発者ブログ</a></td><td>288</td><td>2013/07/08</td></tr>
<tr><td><a href='http://www.publickey1.jp/blog/13/vagrantvagrant_meetup_2013.html' target='_blank'><strong>「Vagrant」は仮想環境をプログラミングするツール。同一環境をどこにでも、いくつでもすぐに作成可能。Vagrant meetup 2013 － Publickey</strong></a></td><td>402</td><td>2013/07/16</td></tr>
<tr><td><a href='http://www.slideshare.net/shin1x1/xampp-mamp-vagrant-php' target='_blank'><strong>もう XAMPP / MAMP はいらない！Vagrant で作る PHP 開発環境</strong></a></td><td>733</td><td>2013/07/18</td></tr>
<tr><td><a href='https://speakerdeck.com/naoya/devopsfalsejin-tokorekara-number-init-devops' target='_blank'>DevOpsの今とこれから #init_devops // Speaker Deck</a></td><td>280</td><td>2013/07/19</td></tr>
<tr><td><a href='https://speakerdeck.com/yandod/chu-metefalsecheffalsejiao-shi-v1-dot-2-chef11dui-ying-ban' target='_blank'>初めてのChefの教室 (v1.2 Chef11対応版) // Speaker Deck</a></td><td>186</td><td>2013/07/20</td></tr>
<tr><td><a href='http://tily.hatenablog.com/entry/2013/07/21/150404' target='_blank'>Chef のレシピから serverspec のテストを自動生成する chef-serverspec-handler という gem を作ってみた - DevOps について書くブログ</a></td><td>143</td><td>2013/07/22</td></tr>
<tr><td><a href='http://k1low.hatenablog.com/entry/2013/07/22/185615' target='_blank'>さくらVPSセットアップ用のシェルスクリプトを今話題の「Ansible」で書き直してみた - Copy/Cut/Paste/Hatena</a></td><td>262</td><td>2013/07/22</td></tr>
<tr><td><a href='http://www.ryuzee.com/contents/blog/6729' target='_blank'>[資料公開]Vagrant (+Amazon EC2) #init_devops | Ryuzee.com</a></td><td>101</td><td>2013/07/23</td></tr>
<tr><td><a href='https://speakerdeck.com/csouls/inhuratimuwochi-tanaihui-she-defalseinhurayun-yong' target='_blank'>インフラチームを持たない会社でのインフラ運用 // Speaker Deck</a></td><td>304</td><td>2013/07/23</td></tr>
<tr><td><a href='http://www.ideaxidea.com/archives/2013/07/basic_chef.html' target='_blank'>『Chef入門 (全14回)』をドットインストールに追加しました #dotinstall | IDEA*IDEA</a></td><td>137</td><td>2013/07/24</td></tr>
<tr><td><a href='http://yteraoka.github.io/ansible-tutorial/' target='_blank'>Ansible Tutorial</a></td><td>138</td><td>2013/07/25</td></tr>
<tr><td><a href='http://dev.classmethod.jp/cloud/aws/aws-jenkins-run-ec2-and-chef-cooking/' target='_blank'>【AWS】JenkinsとserverspecでChefのテストを自動化する ｜ Developers.IO</a></td><td>241</td><td>2013/07/30</td></tr>
</table>

<h3>2013年8月: 「Immutable Infrastracture」</h3>
8月は引き続き活用の事例が話題になっています。特に印象的なのは現在のバズワードである「Immutable Infrastracture」についてのエントリが話題になっていた点です。f440さんのこの記事の書き出しの部分は簡潔にImmutable Infrastractureとはなにか、どのような経緯で話題に上がったかを述べています。

<blockquote>
Immutable Server や Immutable Infrastracture っていう単語がいろんなところで目に入るようになった。とくに Chad Fowler がブログで取り上げたり、Food Fight に出たり して、世間でも関心が高まった感じがある。

プログラムを書く人にはご存じの通り、この Immutable っていうのは状態が変更出来ないことを指している。Immutable な Infrastracture っていうのは、ざっくり言うと「運用中のサーバーに変更を加えない」っていうアプローチでサーバーを管理しているスタイルのこと。
</blockquote>

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://blog.physalis.net/2013/08/09/java-webapp-dev-environment-with-vagrant.html' target='_blank'>Vagrant + Chef で Java Web アプリケーション開発環境を作る - Secret Staircase</a></td><td>117</td><td>2013/08/09</td></tr>
<tr><td><a href='http://apatheia.info/blog/2013/08/10/immutable-infrastructure/' target='_blank'><strong>Immutable Infrastracture について - apatheia.info</strong></a></td><td>189</td><td>2013/08/11</td></tr>
<tr><td><a href='http://ch.nicovideo.jp/dwango-engineer/blomaga/ar311555' target='_blank'>Chef Soloと Knife Soloでの　ニコニコサーバー構築 (1):dwango エンジニア ブロマガ:ドワンゴ研究開発チャンネル(ドワンゴグループのエンジニア) - ニコニコチャンネル:生活</a></td><td>120</td><td>2013/08/12</td></tr>
<tr><td><a href='http://yuuki.hatenablog.com/entry/2013/08/13/220330' target='_blank'>Chefがつらい人のためのAnsibleのはなし - ゆううきブログ</a></td><td>337</td><td>2013/08/13</td></tr>
<tr><td><a href='http://ch.nicovideo.jp/dwango-engineer/blomaga/ar322283' target='_blank'>Chef Soloと Knife Soloでの ニコニコサーバー構築 (2) 〜導入編〜:dwango エンジニア ブロマガ:ドワンゴ研究開発チャンネル(ドワンゴグループのエンジニア) - ニコニコチャンネル:生活</a></td><td>278</td><td>2013/08/22</td></tr>
<tr><td><a href='http://knowledge.sakura.ad.jp/tech/867/' target='_blank'>サーバー設定ツール「Chef」の概要と基礎的な使い方 - さくらのナレッジ</a></td><td>448</td><td>2013/08/26</td></tr>
<tr><td><a href='http://ch.nicovideo.jp/dwango-engineer/blomaga/ar325738' target='_blank'>Chef Soloと Knife Soloでの ニコニコサーバー構築 (3) 〜実行編〜:dwango エンジニア ブロマガ:ドワンゴ研究開発チャンネル(ドワンゴグループのエンジニア) - ニコニコチャンネル:生活</a></td><td>123</td><td>2013/08/26</td></tr>
</table>

<h3>2013年9月: 「アプリケーションエンジニアへのVagrantの普及」</h3>
9月は新しい話題というよりも対象者がChefを使う必要のあるインフラ寄りのエンジニアではなく実際にアプリケーションの開発をするためにVagrantを使うというナレッジが数多く出てきています。アプリケーション開発に実際にVagrantを使い始めたのがこの辺りの時期だった方は結構居るのではないでしょうか。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://hnakamur.github.io/blog/2013/09/01/tried-chef-ansible-fabric/' target='_blank'>Chef-soloとAnsibleとFabricを試した感想 - hnakamur's blog at github</a></td><td>148</td><td>2013/09/02</td></tr>
<tr><td><a href='http://ch.nicovideo.jp/dwango-engineer/blomaga/ar334285' target='_blank'>Chef Soloと Knife Soloでの ニコニコサーバー構築 (4) ～コツ編～:dwango エンジニア ブロマガ:ドワンゴ研究開発チャンネル(ドワンゴグループのエンジニア) - ニコニコチャンネル:生活</a></td><td>153</td><td>2013/09/04</td></tr>
<tr><td><a href='http://dev.classmethod.jp/server-side/chef-vagrant-ruby/' target='_blank'>Chef、Vagrantに興味があるけどRubyをやったことない技術者が最低限知っておいた方がいい知識　まとめ ｜ Developers.IO</a></td><td>293</td><td>2013/09/04</td></tr>
<tr><td><a href='http://www.slideshare.net/marcyterui/aws-2' target='_blank'>小規模SI案件で、 AWS + Chefを使ってみて</a></td><td>193</td><td>2013/09/11</td></tr>
<tr><td><a href='http://shibayu36.hatenablog.com/entry/2013/09/14/192829' target='_blank'>AWS, chef, Cinnamon等を使った無停止デプロイ(PrePAN carton 1.0化の裏側) - $shibayu36->blog;</a></td><td>101</td><td>2013/09/14</td></tr>
<tr><td><a href='http://blog.kentarok.org/entry/2013/09/14/205810' target='_blank'>「PHPアプリケーションの継続的バージョンアップ」という題でPHPカンファレンス2013でトークしてきた #phpcon2013 - delirious thoughts</a></td><td>175</td><td>2013/09/14</td></tr>
<tr><td><a href='http://dev.classmethod.jp/tool/jenkins/jenkins-refactoring-jobs/' target='_blank'>Jenkinsの使い勝手をよくするための見直し6点 ｜ Developers.IO</a></td><td>163</td><td>2013/09/14</td></tr>
<tr><td><a href='http://qiita.com/taiki45/items/b46a2f32248720ec2bae' target='_blank'>Ruby - 今っぽい Vagrant + Chef Solo チュートリアル - Qiita [キータ]</a></td><td>394</td><td>2013/09/15</td></tr>
<tr><td><a href='http://www.1x1.jp/blog/2013/09/php-enviroment-with-vagrant.html' target='_blank'>Vagrantで作るPHP開発環境[実践編]をPHPカンファレンス2013で発表してきた - Shin x blog</a></td><td>223</td><td>2013/09/17</td></tr>
<tr><td><a href='https://speakerdeck.com/yuukit/hatenafalsesabaguan-li-turufalsehua' target='_blank'>はてなのサーバ管理ツールの話 // Speaker Deck</a></td><td>251</td><td>2013/09/21</td></tr>
<tr><td><a href='http://dev.classmethod.jp/referencecat/aws-special/' target='_blank'>AWS 振り返り特集 ｜ Developers.IO</a></td><td>330</td><td>2013/09/26</td></tr>
<tr><td><a href='http://tmtk75.github.io/2013/09/28/docker-jenkins-serverspec-puppet.ja.html' target='_blank'>Docker + Jenkins + serverspecでpuppetのmanifestをCIする</a></td><td>152</td><td>2013/09/29</td></tr>
</table>

<h3>2013年10月: 「メディアで報じられる普及」</h3>
10月に話題になっていた記事にはメディアの記事が2つ含まれています。センセーショナルな見出しだった事もあって多くの方の目を引いたのではないでしょうか。記事には具体的に日本の企業がChefを導入して活用しようとしている事が報じられています。

<blockquote>
サイバーエージェントで消費者向けWebサービスを手がけるアメーバ事業本部では、現時点で20人いるOS/ミドルウエアの運用担当者を、2年後の2015年までにゼロにする計画だ。

　彼らは現在、OS/ミドルウエアをサーバーにインストールしたり、パッチを適用したり、アプリケーションの負荷に応じてサーバー台数を増減したりする業務を行っている。これらの業務を、オープンソースソフトウエアの運用管理ツール「Chef」を導入することで、自動化する計画だ。
</blockquote>

<blockquote>
要注目のツールとして浮かび上がったのが、「Redmine」「Jenkins」「Chef」という三つのオープンソースソフトである。
日経SYSTEMSはこれらを、IT現場の「新3種の神器」と定める。いずれも本格的な普及はこれからという段階だ。しかし、統合開発環境（ビルドツールを含む）やソースコード管理ツールが今どのIT現場でも使われているのと同じように、Redmine、Jenkins、Chefも数年の間に必須のツールとなると予測する。
</blockquote>


<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://www.1x1.jp/blog/2013/10/vagrant-lapp-sample.html' target='_blank'>PHP開発環境のサンプルVagrantfile - Shin x blog</a></td><td>266</td><td>2013/10/09</td></tr>
<tr><td><a href='http://itpro.nikkeibp.co.jp/article/COLUMN/20131002/508384/' target='_blank'><strong>さあ、運用を変えよう - 運用担当者、激減中：ITpro</strong></a></td><td>298</td><td>2013/10/15</td></tr>
<tr><td><a href='http://firegoby.jp/archives/5141' target='_blank'>WordPressのプラグインやテーマ、ウェブサイトの開発に超便利なVagrantつくりました。 | firegoby</a></td><td>372</td><td>2013/10/16</td></tr>
<tr><td><a href='http://www.slideshare.net/pfi/pfi-20130919-linux' target='_blank'>PFIセミナー 2013/09/19 「Linux開発環境の自動構築」</a></td><td>199</td><td>2013/10/19</td></tr>
<tr><td><a href='http://itpro.nikkeibp.co.jp/article/COLUMN/20131017/511814/' target='_blank'><strong>調査で分かった！ITの現場「新3種の神器」 - 新3種の神器を導入しよう：ITpro</strong></a></td><td>124</td><td>2013/10/28</td></tr>
<tr><td><a href='http://mizzy.org/blog/2013/10/29/1/' target='_blank'>インフラ系技術の流れ - Gosuke Miyashita</a></td><td>1036</td><td>2013/10/29</td></tr>
</table>

<h3>2013年11月: 「加速するImmutable Infrastructure」</h3>
11月になると明確にImmutable Infrastructureへの言及が増加します。これによりChefの役割は実際のインスタンスの設定ではなく、Dockerなどのベースを作る為のプロビジョニングツールという形にスライドしていきます。また同時にオーケストレーションツールとしてのSerfにも注目が集まるようになります。
とはいえChefのレシピを記述している人は引き続き多いようで、クックブックの実行サイクルについて解説した記事にアクセスを頂きました。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://www.engineyard.co.jp/blog/2013/vagrant-and-berkshelf/' target='_blank'>nanapi勉強会でVagrant + Berkshelfについて発表しました | Engine Yard Blog JP</a></td><td>108</td><td>2013/11/13</td></tr>
<tr><td><a href='http://orangain.hatenablog.com/entry/jenkins-docker' target='_blank'>Dockerを使ってJenkinsのジョブごとにテスト実行環境を分離する - orangain flavor</a></td><td>155</td><td>2013/11/14</td></tr>
<tr><td><a href='http://suzuken.hatenablog.jp/entry/2013/11/15/171803' target='_blank'>re:InventでのParseのDevOps話がとても良かったのでまとめておく - すずけんメモ</a></td><td>136</td><td>2013/11/15</td></tr>
<tr><td><a href='https://speakerdeck.com/mizzy/future-of-server-provisioning' target='_blank'>Future of server provisioning // Speaker Deck</a></td><td>145</td><td>2013/11/16</td></tr>
<tr><td><a href='http://dqn.sakusakutto.jp/2013/11/php51to54.html' target='_blank'>ソースコード20万行の大規模サイトのPHPを5.1から5.4に上げるためにやったことまとめ - DQNEO起業日記</a></td><td>568</td><td>2013/11/18</td></tr>
<tr><td><a href='http://codezine.jp/article/detail/7484' target='_blank'>構成管理ツール「Chef」の概要とインストール手順 （1/4）：CodeZine</a></td><td>464</td><td>2013/11/18</td></tr>
<tr><td><a href='http://blog.mirakui.com/entry/2013/11/21/reinvent-immutable-infrastructure' target='_blank'>AWS re:Invent と Immutable Infrastructure - 昼メシ物語</a></td><td>178</td><td>2013/11/21</td></tr>
<tr><td><a href='http://togetter.com/li/594684' target='_blank'>Immutable Infrastructure の有用性 - Togetter</a></td><td>144</td><td>2013/11/25</td></tr>
<tr><td><a href='http://blog.glidenote.com/blog/2013/11/26/sensu/' target='_blank'>監視ソフトをNagiosからSensuに切り替えて2ヶ月経ったのでまとめた - Glide Note - グライドノート</a></td><td>548</td><td>2013/11/26</td></tr>
<tr><td><a href='http://blog.mirakui.com/entry/2013/11/26/231658' target='_blank'>今さら聞けない Immutable Infrastructure - 昼メシ物語</a></td><td>514</td><td>2013/11/26</td></tr>
<tr><td><a href='https://speakerdeck.com/aereal/vagrant-to-chef-detukuruhatenabutukumakufalsekai-fa-huan-jing' target='_blank'>Vagrant と Chef でつくるはてなブックマークの開発環境 // Speaker Deck</a></td><td>201</td><td>2013/11/27</td></tr>
<tr><td><a href='http://www.engineyard.co.jp/blog/2013/chef-recipe-lifecycle/' target='_blank'><strong>Chefのレシピは上から下に実行されるという誤解 | Engine Yard Blog JP</strong></a></td><td>255</td><td>2013/11/28</td></tr>
</table>

<h3>2013年12月: 「OpsCode社の社名がChefに」</h3>
そして現在でもある12月。Chefが脚光を浴びたことで始まった一連の流れは改めて「Infrastructure as Code」の文脈で整理されています。これまでの流れを見てもわかるように、Chefを単体で使う事に意味があるのではなくプロビジョニングをコード化し、継続的にテストし、Immutable Infrastructureのような運用性を実現する事が肝要です。
直接話題になる事はすくなった部分もありますがクックブックを継続的にテストする事やワークフローの改善が今後も浸透していくのではないでしょうか。

<table>
<tr><th>記事</th><th>users数</th><th>登録日</th></tr>
<tr><td><a href='http://blog.kentarok.org/entry/2013/12/01/221729' target='_blank'>Immutable Infrastructure時代のConfiguration Management Toolの要件およびその実装について - delirious thoughts</a></td><td>172</td><td>2013/12/01</td></tr>
<tr><td><a href='http://www.slideshare.net/KojiHasebe/2-v2-28915618' target='_blank'>プライベートクラウド作ってみました</a></td><td>278</td><td>2013/12/05</td></tr>
<tr><td><a href='http://www.publickey1.jp/blog/13/chefopscodechef.html' target='_blank'><strong>Chef開発元のOpscode、社名をChefに変更。「検索が難しくなる」とあちこちで悲鳴が － Publickey</strong></a></td><td>105</td><td>2013/12/11</td></tr>
<tr><td><a href='http://wadap.hatenablog.com/entry/2013/12/15/155024' target='_blank'>さくらVPSを使って便利な開発環境を構築する - UNIX的なアレ</a></td><td>525</td><td>2013/12/15</td></tr>
<tr><td><a href='http://d.hatena.ne.jp/naoya/20131215/1387090668' target='_blank'><strong>Infrastructure as Code - naoyaのはてなダイアリー</strong></a></td><td>462</td><td>2013/12/15</td></tr>
</table>

<h3>おまけ：Chefに関する情報源</h3>
短期的に話題になった情報ではないですが、特に下記のコンテンツは量も豊富かつ正確なので参照するとよいでしょう。

<ul>
<li>Rubyist Magazine - Chef でサーバ管理を楽チンにしよう！ (第 1 回)
<a href="http://magazine.rubyist.net/?0035-ChefInDECOLOG" target="_blank">http://magazine.rubyist.net/?0035-ChefInDECOLOG</a></li>
<li>Opscode Open Source Wiki(情報が古いが日本語の情報)
<a href="https://wiki.opscode.com/pages/viewpage.action?pageId=24019581" target="_blank">https://wiki.opscode.com/pages/viewpage.action?pageId=24019581</a></li>
<li>Chefについてのドキュメント(英語)
<a href="http://docs.opscode.com/" target="_blank">http://docs.opscode.com/</a></li>
<li>Resources and Providers Reference — Chef 
<a href="http://docs.opscode.com/chef/resources.html" target="_blank">http://docs.opscode.com/chef/resources.html</a></li>
<li>Recipe DSL — Chef 
<a href="http://docs.opscode.com/chef/dsl_recipe.html" target="_blank">http://docs.opscode.com/chef/dsl_recipe.html</a></li>
<li>Esseintials nodes chef run
<a href="http://docs.opscode.com/essentials_nodes_chef_run.html" target="_blank">http://docs.opscode.com/essentials_nodes_chef_run.html</a></li>
</ul>

<h3>動画で振り返る「Chef ゆく年くる年」</h3>
<iframe width="853" height="480" src="//www.youtube.com/embed/zuw2kwZOAjA" frameborder="0" allowfullscreen></iframe>

<hr/>
<a href="http://ey.io/noyakshave"><img src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png"></a>
