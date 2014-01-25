---
layout: post
status: publish
published: true
title: リソース指向のWebアプリ 〜Nate Abele氏 来日講演〜
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1278
wordpress_url: http://www.engineyard.co.jp/blog/?p=1278
date: 2013-08-01 12:51:29.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/08/DSC03559-1024x682.jpg" alt="DSC03559" width="1024" height="682" class="alignnone size-large wp-image-1279" />

PHPの人気フレームワーク、CakePHPやLithiumのリードデベロッパーを努め、現在はAngularUIでも精力的に開発を行なっているNate Abele氏が来日し、Engine Yardにて講演を行なってくれました。当初はバージョン1.0のリリースが間近のLithiumについての講演かと思われていましたが、実際のところは<strong>RESTなサーバーサイドをLithiumで実装し、インターフェースをAngularJSで実装する</strong>という意欲的な手法についての講演でした。

<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;"><strong>緊急開催 Lithium Tokyo 〜Nate Abele氏来日イベント〜</strong><br>
<a href="http://atnd.org/events/41843">http://atnd.org/events/41843</a><br>
<strong>つぶやきのまとめ</strong>
<a href="http://togetter.com/li/541759">Nate Abele氏来日講演 リソース指向開発 Lithium + AngularJS - Togetter</a>
</p>

<h3>AngularJSとは？</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/08/Resource-Oriented_Applications_with_AngularJS_and_Lithium.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/08/Resource-Oriented_Applications_with_AngularJS_and_Lithium-1024x742.png" alt="Resource-Oriented_Applications_with_AngularJS_and_Lithium" width="1024" height="742" class="alignnone size-large wp-image-1287" /></a>

AngularJSはJQueryをベースに更に抽象化し、動的なユーザーインターフェースを実装しやすくするフレームワークです。同様のプロジェクトとしては<a href="http://backbonejs.org/" target="_blank">Backbone.js</a>や<a href="http://emberjs.com/" target="_blank">Ember.js</a>などが知られています。Angular.jsはGoogleが中心に開発されていおり、人気があります。

<table style="width:60%">
<tr>
<th>Name</th>
<th>Star on GitHub</th>
</tr>
<tr>
<td>AngularJS</td>
<td>12304</td>
</tr>
<tr>
<td>Backbone.js</td>
<td>15157</td>
</tr>
<tr>
<td>Ember.js</td>
<td>7625</td>
</tr>
</table>

AngularJSを使うとイベントに対応してインターフェースを更新する処理や、リモートのAPIを経由したリソースの操作をシンプルな実装で実現できます。例えばキー入力を検知してページに内容を反映するコードをJQueryで記述した場合は下記のようになります。

<pre lang="html">
<input type="text" id="name">
<h1>Hello!</h1>

<script type="text/javascript">
    $(document).ready(function() {
        $('#name').keydown(function(e) {
            $('h1').html("Hello " + e.target.value + "!")
        });
    });
</script>
</pre>

JQueryのサポートを受けているとはいえ、イベントを元にDOMに対して操作を行うという記述が必要になっています。ユーザーインターフェースの要素が多くなるにつれJavaScriptのコード量が増えてしまう事になります。同じ動作をAngularJSで記述すると次のようになります。

<pre lang="html">
<input type="text" ng:model="name">
<h1>Hello {{ name }}!</h1>
</pre>

圧倒的に記述が少なくなっているのが分かります。AngularJSのngModelの機能を使いデータをバインディングする事でリアルタイムに各所にデータを反映する事ができています。Nateの発表資料そのものもAngularJSを使って記述されたアプリケーションになっており、スライド内でサンプルが直接動作するという内容になっていました。またngResourceを使うことでオブジェクトを操作するだけで対応するRESTなAPIを操作してサーバーサイドと通信する事もできます。
これによりリソースという概念を通じてフロントエンドのJavaScriptアプリケーションとバックエンドのPHPアプリケーションを疎結合にすることができます。

<h3>何故、リソース指向に進むのか</h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/08/DSC03569-1024x682.jpg" alt="DSC03569" width="1024" height="682" class="alignnone size-large wp-image-1296" />

リソース指向でアプリケーションを開発する事により、PHPのアプリケーション側は基本的にRESTなAPIを提供するだけの構成となります。従来はビューテンプレートやヘルパーを利用して行なっていたデータをHTMLに反映するといった記述は一切なくなります。Lithiumの場合はモデルの内容をリソースとして自動的に提供するプラグインを活用する事で<span style="color:red"><strong>PHP側のソースコードからはコントローラーもビューも無くなります。</strong></span>
モデル層とユーザーインターフェースをつなぐインターフェースがリソースとして標準化された事でその部分のコードが消滅し、コードの総量はサーバーサイドのMVCアプリケーションの際よりも更に削減されることになります。

このアグレッシブすぎるようにも見えるアプローチですが、話を聞いているとかつて彼がCakePHPから離脱した際に書いた言葉を思い出しました。

<blockquote>人は変化を嫌う事が多い。そう、先に進む事よりも恐れる事を選ぶ。なぜなら恐れるのは簡単だからだ。特に意志も努力も必要はない。目新しい事ではないが、我々は簡単にそれを忘れてしまう。僕はこんな話を聞いた事がある。<strong>もし君が2年前に書いたコードや1年前に書いたコード、あるいは数カ月前に書いたコードを見て少しでもそれを放り出したいと思わなければ君は全く進歩していない。</strong>ソフトウェア開発が職人芸だと思う僕らにとってはこれはとても意味深い。
<a href="http://blog.candycane.jp/archives/121">変化の時(Nate AbeleがCakePHPプロジェクトから離脱してLithiumを立ち上げた理由) : candycane development blog</a>
</blockquote>

変化はすぐに起きるわけではないでしょう。ですがMVCフレームワークを使ってサーバーサイドでHTMLを動的に生成する為のコードを大量に記述するというアプローチが過去のものになっていく可能性は決して低くないのではないでしょうか。


<h3>講演の資料と動画</h3>
講演の資料と動画は下記のとおりです。今後のWebアプリケーション開発の手法について考えるきっかけになるとてもよい講演ですので、是非ご覧ください。

<a href="http://li3-angular.lithium-framework.com/#/9"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/08/Resource-Oriented_Applications_with_AngularJS_and_Lithium1-1024x741.png" alt="Resource-Oriented_Applications_with_AngularJS_and_Lithium" width="1024" height="741" class="alignnone size-large wp-image-1303" /></a>

<iframe width="853" height="480" src="//www.youtube.com/embed/FVGS_1AYjvA" frameborder="0" allowfullscreen></iframe>

<iframe width="853" height="480" src="//www.youtube.com/embed/QSrZ-pnUkeQ" frameborder="0" allowfullscreen></iframe>

<iframe width="853" height="480" src="//www.youtube.com/embed/D3PD6DMG9vQ" frameborder="0" allowfullscreen></iframe>

<hr>

Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。PHPを利用したアプリケーションをデプロイする際は、Engine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>
