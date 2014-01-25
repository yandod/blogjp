---
layout: post
status: publish
published: true
title: 'PHPのベストプラクティス"The Right Way"の資料 #phpstudy'
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 955
wordpress_url: http://www.engineyard.co.jp/blog/?p=955
date: 2013-04-23 10:51:10.000000000 +09:00
categories:
- Uncategorized
tags: []
comments:
- id: 60
  author: モダンPHPチュートリアルを開催しました | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/modern-php-tutorial/
  date: '2013-08-26 14:33:05 +0900'
  date_gmt: '2013-08-26 05:33:05 +0900'
  content: '[...] PHPのベストプラクティス”The Right Way”の資料 #phpstudy | Engine Yard Blog JP
    http://www.engineyard.co.jp/blog/2013/php-the-right-way/ [...]'
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/DSC00566-1024x682.jpg" alt="DSC00566" width="1024" height="682" class="alignnone size-large wp-image-956" />

昨日の第67回 PHP勉強会でPHPのベストプラクティスとして公開されている<a href="http://ja.phptherightway.com/">PHP: The Right Way</a>について発表を行いました。発表はあくまで全体を眺めるという感じで細かい所までは言及できていませんので少しここで補足をしておきます。

<h4>基本のコーディングは大事</h4>
<a href="http://ja.phptherightway.com/pages/The-Basics.html" target="_blank">基本</a>として提示されているPHPのコーディングはとても参考になります。発表でも触れましたが比較演算子や条件分岐、日付処理の扱いなどを見るだけで書き手のPHPのレベルは丸わかりと言ってもいいかもしれません。いくつか抜粋してみます。

<h5>曖昧な比較を用いた失敗</h5>
<pre lang="php">
<?php
/**
 * 厳格な比較
 */
if (strpos('testing', 'test')) {    // 'test' は 0 番目の位置にあり、これはboolean型の'false'と見なされる
    // コード...
}
</pre>
strposは検索文字列を発見できないとFALSEを返します。この場合先頭に対象文字列があるので0が返りますが、厳密な比較を用いていないが為に意図した動きになりません。

<h5>無駄なelse</h5>
<pre lang="php">
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}
</pre>
このelseは意味がありません。無駄にインデントが深くなっているだけですね。

<h5>DateTime(これは良い例)</h5>
<pre lang="php">
<?php
$raw = '22. 11. 1968';
$start = \DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start date: ' . $start->format('m/d/Y') . "\n";
</pre>

この例で示されているような文字列を分割したりしてmktimeで処理するというようなコードを初心者の人は良く書いてしまいがちです。見ての通り実は組み込みのモジュールを使えばどうとでも処理することができます。

<h4>その他</h4>
最近はComposerを使うとコードの再利用がいい感じなりますし、autoloadも存分に活用できます。まだ充分に利用が広まっていないのが残念ですが、使っていない場合は楽をするために活用したいところです。あちこちにrequire_onceをばら撒く労力はもう必要なくなったのです。(require_onceではなくrequireを使っているなんていうのはまた別の話ですが...)

<h4>スライドと動画</h4>
<script async class="speakerdeck-embed" data-id="435f5cf08bbe0130611e1231381d54e9" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

<iframe width="720" height="437" src="http://www.ustream.tv/embed/recorded/31816357?v=3&amp;wmode=direct" scrolling="no" frameborder="0" style="border: 0px none transparent;">    </iframe>
<br /><a href="http://www.ustream.tv/" style="padding: 2px 0px 4px; width: 400px; background: #ffffff; display: block; color: #000000; font-weight: normal; font-size: 10px; text-decoration: underline; text-align: center;" target="_blank">Video streaming by Ustream</a>

次回も第4月曜日に開催の予定です。運営スタッフの皆様、発表者の皆様、参加者のみなさまお疲れ様でした。

<div style="text-align:center"><a href="http://www.engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></div>
