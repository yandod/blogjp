---
layout: post
status: publish
published: true
title: PHPの教室「foreachを極める」を開催しました
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 482
wordpress_url: http://www.engineyard.co.jp/blog/?p=482
date: 2013-01-25 09:14:22.000000000 +09:00
categories:
- Uncategorized
tags: []
comments:
- id: 21
  author: 2013年2月2日のヘッドライン | WP-D
  author_email: ''
  author_url: http://wp-d.org/2013/02/02/2378/
  date: '2013-02-02 18:22:49 +0900'
  date_gmt: '2013-02-02 09:22:49 +0900'
  content: '[...] PHPの教室「foreachを極める」を開催しました &#8211; Engine Yard Blog JP | Engine
    Yard... [...]'
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/01/phpの教室.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/01/phpの教室-300x300.png" alt="" title="phpの教室" width="300" height="300" class="alignnone size-medium wp-image-483" /></a>

不定期で開催しているPHPに関するレッスン、「PHPの教室」を1月22日(火)に下北沢オープンソースカフェで開催しました。今回は現地参加は4名でしたが、ライブ配信を20人ほどの人が見ており事後に公開したスライドもじわじわと閲覧されているようでなんだかんだで盛況でした。

foreachはPHPでも特に頻繁に使われる構文ですが、頻繁に利用されるが故に技術的な負債を作ってしまうような使い方をしているとコードベースのメンテナンス性を大きく損ないます。講義の中でも触れていますが、エラー処理の考慮漏れや、参照代入を利用したトリッキーな書き方、深すぎるネストなどPHPのコードを書く人であればだれもが気をつけるべき問題です。

<h2>実際のコード例の抜粋</h2>

foreachのループ内で一時的な変数を更新する処理は変数がオブジェクトかどうかや＆を使った参照代入をするかによって結果が異なります。変数の中身や＆の有無などを読み落としただけで想定と異なる挙動をする為非常に扱いにくいコードになりがちです。

<strong>$rowはコピーされているので$listは更新されない例</strong>
<pre>
&lt;?php
$list = array('ごはん','ナン','麺');
foreach ( $list as $key => $row ) {
  $row = 'チョコ';
}
</pre>

<strong>$rowに参照代入されているので$listが全て「チョコ」に更新される例</strong>
<pre>
&lt;?php
$list = array('ごはん','ナン','麺');
foreach ( $list as $key => &$row ) {
  $row = 'チョコ';
}
</pre>

<strong>$rowはオブジェクトなので参照となり、$listの内容が全て「チョコ」に更新される例</strong>
<pre>
&lt;?php
$list = array(
  new stdClass(),
  new stdClass(),
  new stdClass()
);
$list[0]->name = 'ごはん';
$list[1]->name = 'ナン';
$list[2]->name = '麺';

foreach ( $list as $key => $row ) {
  $row->name = 'チョコ';
}
</pre>

たとえ上記のコードの挙動の違いを完全に把握していたとしても、ちょっとした見落としや勘違いだけでプログラムの挙動が大きく変わってしまいます。メンテナンス性を考慮すると&を使った参照代入や一時変数に対する更新処理は避けるのが無難です。更新が必要なのであればループの素になっている配列を直接指定して更新する事で全ての場合で同じ挙動となります。

<strong>ループに渡されている配列を直接更新する例</strong>
<pre>
&lt;?php
$list = array('ごはん','ナン','麺');
foreach ( $list as $key => $row ) {
  $list[$key] = 'チョコ';
}
</pre>

一見するとなんてことのない4つのコードですが、内容の違いを理解してメンテナンス性の高いコードを書いていけるように心がけていきましょう。(&を使った参照代入はPHP4時代を生き抜く為の知恵であって、現在はレガシーコードと化している場合が殆どでしょう。)講演では他にもさまざまなコード例やイテレーターやジェネレーターを使った記述の例についても取り上げています。特にジェネレーターについては自分自身にとっても有意義だったなと感じていますので、<strong>PHP5.5でジェネレーターを動かした事のない方には一見して頂きたい</strong>なと思っています。

<h2>講演の資料</h2>

<strong>スライド</strong>
<iframe src="http://www.slideshare.net/slideshow/embed_code/16110047" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen webkitallowfullscreen mozallowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="http://www.slideshare.net/yandod/phpforeach" title="PHPの教室「foreachを極める」" target="_blank">PHPの教室「foreachを極める」</a> </strong> from <strong><a href="http://www.slideshare.net/yandod" target="_blank">yandod</a></strong> </div>

<strong>動画</strong>
<a href="http://new.livestream.com/shimokitazawa-osscafe/shimokita-php/videos/9891154" target="_blank">http://new.livestream.com/shimokitazawa-osscafe/shimokita-php/videos/9891154</a>

<strong>サンプルコード</strong>
<a href="https://github.com/yandod/php-foreach">yandod/php-foreach · GitHub</a>

<a href="http://engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/01/300x250-banner-paas-300x234.png" alt="" title="300x250-banner-paas" width="300" height="234" class="alignnone size-medium wp-image-489" /></a>
