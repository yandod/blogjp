---
layout: post
status: publish
published: true
title: PHPのエラーに関する講演の資料
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 81
wordpress_url: http://www.engineyard.co.jp/blog/?p=81
date: 2012-10-17 14:53:14.000000000 +09:00
categories:
- Uncategorized
tags:
- PHP
- コミュニティ
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/error.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/error.png" alt="" title="error" width="636" height="473" class="alignnone size-full wp-image-82" /></a>

安藤です。下北沢オープンソースカフェで隔週火曜日に開催されているPHPのコミュニティ、Shimokita.phpでPHPのエラーに関するセッションを行いました。実際の開発やプロダクトのセットアップ時に目にする事の多いエラーですが、その種類や対処方法についてじっくり考える機会は意外と少ないのではないでしょうか。

今回のセッションでは下記のような点を紹介しています。

<ul>
	<li><strong>各種エラーの種類と原因</strong>
FatalやNoticeなど一見するとちょっとした違いに見えますが、残りの処理が実行されるかどうかや発生原因は大きく異なります。</li>
	<li><strong>エラーに関する設定項目</strong>
エラーメッセージが画面に表示されるかログに記録されるかといった挙動は設定によって異なります。正しい設定が行われていないと不適切な情報がユーザに表示されたり、運用環境で障害が発生している事に気が付かないといった問題があります。開発環境と運用環境に適切な設定を行うように気をつけましょう。</li>
	<li><strong>エラーハンドリング</strong>
動作中に発生したエラーを効率的に扱う為に有効なのがエラーハンドリングです。エラー発生時に自動的に行われる処理を活用する事で少ないコードでエラー発生時の挙動を担保できます。</li>
	<li><strong>例外処理の概要</strong>
PHP5から利用できるようになった例外処理はエラー発生時の処理をより効率的に実装できます。一方で誤った実装を行なわれている例が非常に多い機能です。挙動だけでなく、失敗例などについても把握をしておきましょう。</li>
</ul>

スライドについてはSlideShareにアップロードしていますのでこちらをどうぞ。
<iframe src="http://www.slideshare.net/slideshow/embed_code/14760315" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="http://www.slideshare.net/yandod/90-php" title="90分間濃縮 PHPエラーの教室" target="_blank">90分間濃縮 PHPエラーの教室</a> </strong> from <strong><a href="http://www.slideshare.net/yandod" target="_blank">yandod</a></strong> </div>
