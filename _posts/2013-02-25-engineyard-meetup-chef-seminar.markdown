---
layout: post
status: publish
published: true
title: 「初めてのChefの教室」を開催しました。(動画&資料)
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 552
wordpress_url: http://www.engineyard.co.jp/blog/?p=552
date: 2013-02-25 10:46:51.000000000 +09:00
categories:
- Uncategorized
tags: []
comments:
- id: 28
  author: 今もっとも学習コスパの高い技術はChefだと、Chef勉強会に行って確信した - akiyan.com
  author_email: ''
  author_url: http://www.akiyan.com/blog/archives/2013/02/chef-is-the-technology-in-which-study-cost-performance-is-the-highest-now.html
  date: '2013-02-25 12:53:32 +0900'
  date_gmt: '2013-02-25 03:53:32 +0900'
  content: '[...] 株式会社Engine Yard主催の、Chef(opschef)勉強会第一回「初めてのChefの教室 #eytokyo」に行って来ました。勉強会の全編動画は、「初めてのChefの教室」を開催しました。(動画&amp;資料)
    - Engine Yard Blog JP | E... で観ることができます。  [...]'
- id: 33
  author: 技術勉強会等へ会場提供を行なっています - Engine Yard Blog JP | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/call-for-meetup-at-engineyard/
  date: '2013-03-29 15:39:48 +0900'
  date_gmt: '2013-03-29 06:39:48 +0900'
  content: '[...] 初めてのChefの教室 [...]'
- id: 51
  author: 「初めてのChefの教室」をアップデートしました | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/chef-tutorial-updated/
  date: '2013-07-06 15:09:11 +0900'
  date_gmt: '2013-07-06 06:09:11 +0900'
  content: '[...] 「初めてのChefの教室」を開催しました。(動画&amp;資料) http://www.engineyard.co.jp/blog/2013/engineyard-meetup-chef-seminar/
    [...]'
- id: 90
  author: Chefのレシピは上から下に実行されるという誤解 | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/chef-recipe-lifecycle/
  date: '2013-11-28 17:12:43 +0900'
  date_gmt: '2013-11-28 08:12:43 +0900'
  content: '[&#8230;] 「初めてのChefの教室」を開催しました。(動画&amp;資料) | Engine Yard Blog JP http://www.engineyard.co.jp/blog/2013/engineyard-meetup-chef-seminar/
    [&#8230;]'
- id: 107
  author: 2013年Chefの話題を一挙に振り返るまとめ | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/year-of-chef/
  date: '2013-12-18 13:55:42 +0900'
  date_gmt: '2013-12-18 04:55:42 +0900'
  content: '[&#8230;] 「初めてのChefの教室」を開催しました。(動画&amp;資料) &#8211; Engine Yard Blog&#8230;
    [&#8230;]'
- id: 155
  author: '2013年を振り返る (75投稿 26講演 475貢献 2オキュラス) : candycane development blog'
  author_email: ''
  author_url: http://blog.candycane.jp/archives/2000
  date: '2013-12-31 14:34:21 +0900'
  date_gmt: '2013-12-31 05:34:21 +0900'
  content: '[&#8230;] 「初めてのChefの教室」を開催しました。(動画&amp;資料) | Engine Yard Blog JP GitHubのJohn
    Britton氏によるGitのレッスン | Engine Yard Blog JP Chefのレシピは上から下に実行されるという誤解 | Engine Yard
    Blog JP [&#8230;]'
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/02/480169_489032077821539_1268681057_n.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/02/480169_489032077821539_1268681057_n.jpg" alt="" title="480169_489032077821539_1268681057_n" width="960" height="720" class="alignnone size-full wp-image-553" /></a>

　去る2/22(金)に恵比寿の弊社オフィスにて初の勉強会となる「<a href="http://kokucheese.com/event/index/74459/" target="_blank">初めてのChefの教室</a>」を開催しました。インフラエンジニアだけでなく、アプリケーションエンジニアからも注目が集まっているChefの勉強会という事で様々な方にお集まり頂き、濃い情報交換が繰り広げられました。
　この記事では内容のまとめてスライドや動画などの各種資料を集約します。さらに公開された記事などの資料も順次追加していきます。

<h2>Chef未経験者向けのセッション</h2>
<iframe src="http://player.vimeo.com/video/60361561" width="500" height="281" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe> <p><a href="http://vimeo.com/60361561">[eytokyo] 初めてのChefの教室</a> from <a href="http://vimeo.com/suzuki">suzuki</a> on <a href="http://vimeo.com">Vimeo</a>.</p>

<script async class="speakerdeck-embed" data-id="094a5890611801308ce41231381a7080" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

　まずは最初のセッションとしてRubyもChefも未経験な人(≒PHPer)向けのChefのセッションをyandoが担当しました。セッションではChefの動作原理やアーキテクチャの全体像を示した上で、<strong>最低限レシピを書いて実行する為に必要な手順だけ</strong>をデモを交えて紹介しました。また実際に公開されているレシピの内容やセットアップ時に気になる点などについて会場からもいろいろと反応を貰うことができたので、概ねChefを初めて使う人にとっては適切な内容である事を参加者の皆さんにレビューして頂けたのではと思います。

<table>
  <tr>
    <th>内容</th>
    <th>再生時間</th>
  </tr>
  <tr>
    <td>はじめに</td>
    <td>00:00:00</td>
  </tr>
  <tr>
    <td>セットアップ</td>
    <td>00:11:40</td>
  </tr>
  <tr>
    <td>セットアップのデモ</td>
    <td>00:23:49</td>
  </tr>
  <tr>
    <td>レシピの記述</td>
    <td>00:36:18</td>
  </tr>
  <tr>
    <td>情報の探し方</td>
    <td>00:54:45</td>
  </tr>
</table>

<!-- -->

<h2>超豪華なメンバーによるLT</h2>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/02/859294_277535169044078_1639743555_o.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/02/859294_277535169044078_1639743555_o-300x225.jpg" alt="" title="859294_277535169044078_1639743555_o" width="300" height="225" class="alignnone size-medium wp-image-603" /></a>

<iframe src="http://player.vimeo.com/video/60361566" width="500" height="281" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe> <p><a href="http://vimeo.com/60361566">[eytokyo] Lightning Talks</a> from <a href="http://vimeo.com/suzuki">suzuki</a> on <a href="http://vimeo.com">Vimeo</a>.</p>

　続いて休憩を挟んで超豪華な顔ぶれによるLT大会を行いました。どの講演者の方もChefに関する雑誌やブログの記事を書かれた方や実際に業務で利用している方など非常に耳寄りな講演でした。質疑応答に対する質問も鋭い質問がいくつも寄せられ、会場からも回答が出るなどまさに「意見交換」といった雰囲気に講演者の方も参加者の方も満足気にしていたのが印象的です。

<table>
  <tr>
    <th>タイトル</th>
    <th>発表者</th>
    <th>再生時間</th>
  </tr>
  <tr>
    <td>Chefの最新動向</td>
    <td>堀田直孝</td>
    <td>00:00:00</td>
  </tr>
  <tr>
    <td>Chef/AWS OpsWorksを使った簡単環境構築</td>
    <td>舟崎健治</td>
    <td>00:10:10</td>
  </tr>
  <tr>
    <td>ソーシャルアプリケーション基盤におけるchef導入</td>
    <td>千葉則行</td>
    <td>00:29:40</td>
  </tr>
  <tr>
    <td>はじめて、VPSをchef-soloで管理してみた</td>
    <td>個々一番</td>
    <td>00:40:56</td>
  </tr>
  <tr>
    <td>Cookbook作りでハマったところ</td>
    <td>菅井祐太朗</td>
    <td>00:48:43</td>
  </tr>
  <tr>
    <td>vagrant + chef</td>
    <td>伊藤直也</td>
    <td>00:55:04</td>
  </tr>
  <tr>
    <td>3分でわかる(気になれる)AWS OpsWorks</td>
    <td>並河祐貴</td>
    <td>01:02:18</td>
  </tr>
</table>

<strong>話題になった台詞</strong>
「いつやるの、Chefでしょ！」
「背景はイメージです(DQ10 全職業 Lv60.)」
「マズイことが起こりました…(大トリなのにネタが被った)」

<strong>発表者の方々の資料へのリンク</strong>
<ul>
<li>Chefの最新情報(仮) (堀田直孝)</li>
<li>Chef/AWS OpsWorksを使った簡単環境構築 (舟崎健治)</li>
<li>ソーシャルゲーム基盤におけるchef導入の取組み (千葉則行)</li>
<li>はじめて、VPSをchef-soloで管理してみた (個々一番)</li>
<li>Cookbook作りでハマったところ(仮) (菅井祐太朗) 
<a href="http://d.hatena.ne.jp/lncr_ct9a/20130223/1361597781">Chef勉強会@Engine Yardさんに行ってきた - 実はhokkai7go</a></li>
<li>vagrant + chef で安全に cookbook を調整 (伊藤直也)
<a href="http://d.hatena.ne.jp/naoya/20130223/1361583027">chef 勉強会 - naoyaのはてなダイアリー</a></li>
<li>タイトル未定 (並河祐貴)
<a href="http://d.hatena.ne.jp/rx7/20130222/p1">「3分でわかる(気になれる)AWS OpsWorks」のLT資料を公開します - 元RX-7乗りの適当な日々</a></li>
</ul>

<strong>その他の記事など</strong>
<ul>
<li><a href="http://togetter.com/li/460798?f=tgtn">初めてのChefの教室へのツイート - Togetter</a></li>
<li><a href="http://ameblo.jp/goodoo/entry-11476465195.html">VagrantとChef-soloで鼻血出す｜渋谷で働くソーシャルアプリエンジニアのブログ</a></li>
<li><a href="http://chiastolite.github.com/blog/2013/02/23/chef-for-beginners/">Chefの勉強会に行ってきた - akadama</a></li>
<li><a href="http://www.akiyan.com/blog/archives/2013/02/chef-is-the-technology-in-which-study-cost-performance-is-the-highest-now.html">今もっとも学習コスパの高い技術はChefだと、Chef勉強会に行って確信した - akiyan.com</a></li>
<li><a href="http://yu-hi.babymilk.jp/wp/it/chef/%E3%80%8C%E5%88%9D%E3%82%81%E3%81%A6%E3%81%AEchef%E3%81%AE%E6%95%99%E5%AE%A4%E3%80%8D%E3%81%AFchef%E5%88%9D%E5%BF%83%E8%80%85%E3%81%AB%E3%81%A8%E3%81%A3%E3%81%A6%E3%82%82%E3%82%88%E3%81%84%E3%80%82/">「初めてのChefの教室」はChef初心者にとってもよい。</a></li>
<li><a href="http://suzuki.tdiary.net/20130225.html#p01">[雑] 「初めてのChefの教室」の録画を Vimeo にアップしたらアクセスが伸びまくり - 雑文発散(2013-02-25)</a></li>
<li><a href="http://hatch2.com/blog/archives/1866">ImpArt » Chef勉強会に参加しました</a></li>
<li><a href="http://iakio.hatenablog.com/entry/2013/02/23/204737">Chef勉強会をUstで見てた - iakioの日記</a></li>
<li><a href="http://hogehoge.hateblo.jp/entry/2013/02/23/140445">PHPerにもできた。はじめてのChef勉強会に行ってきた。 - とあるななしの備忘録</a></li>
<li><a href="http://box406.hatenablog.com/entry/2013/02/26/113246">「初めてのchefの教室」をみてvagrantとchefを使ってみる　第1回 - ロックとチュウーハイとこりんがるな日々</a></li>
<li><a href="http://makies.hatenablog.com/entry/2013/02/25/140238">Chef勉強会 をustで見た #opschef - 書き置き。</a></li>
</ul>

<h2>今後について</h2>
　ひとまずは今回の開催に集中していたのでその後の展望は考えていませんでしたが、今回の発表内容からほとんどの人がVagrantに注目している事が見えて来ましたので、<span style="color:red"><strong>Vagrantに注目した形での第2回というのはいいかもしれない</strong></span>と思っています。また参加者の中にRuby未経験者が半分程度居たので<span style="color:red"><strong>「非Rubyistの為のRubygems」のような内容</strong></span>も考えています。もちろんPaaSに関する内容も候補になりますね。いずれにせよ皆さんからのフィードバックを元に検討できればと思いますので、ご要望などをお聞き出来ればと思います。

<h2>One more thing..</h2>
Engine Yard Cloudには<a href="http://www.engineyard.co.jp/blog/2012/introducing-engine-yard-local/" target="_blank">クラウド上と同じインスタンスをローカル環境上に作成するEngine Yard Local</a>というツールを公開しています。このツールは話題に上がったVagrantを使ってクラウド上と同じ環境を構築するという事でChefとVagrantを使った運用とクラウド環境を透過的に扱えるなかなかスグレモノのツールです。こちらについてはVagrant中心の勉強会を行う際にはご紹介できればよいなと思っています。

<a href="https://www.facebook.com/eyjapan"><strong>技術イベントの情報やその他の最新情報をFacebookで更新しています。宜しければ「イイね」をお願いします</strong></a>
