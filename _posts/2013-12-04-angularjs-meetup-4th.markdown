---
layout: post
status: publish
published: true
title: 'AngularJS 勉強会のまとめ (動画・スライド) #ng_jp'
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 2031
wordpress_url: http://www.engineyard.co.jp/blog/?p=2031
date: 2013-12-04 14:47:57.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/DSC06688-1024x682.jpg" alt="DSC06688" width="1024" height="682" class="alignnone size-large wp-image-2059" />
AngularJSの勉強会に参加して来ました。300人の定員があっという間に満席になるという事で注目の高さが伺える勉強会でした。参加者も発表の内容もバラエティに富んでいてこれから大きな飛躍があるであろう事を期待させる盛りだくさんの内容でした。
今回はEngine Yardから懇親会のスポンサードをさせて頂くと同時にPHPとAngularJSの連携のLTや動画の撮影を行ってきましたので紹介させて頂きます。

<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;">
<strong>ng-mtg#4 AngularJS 勉強会 | 集客ならイベントアテンド</strong><br/><a href="http://atnd.org/event/E0021975/" target="_blank">http://atnd.org/event/E0021975/</a>
<strong>ng-mtg#4 AngularJS 勉強会 #ng_jp - Togetterまとめ</strong><br/><a href="http://togetter.com/li/598391" target="_blank">http://togetter.com/li/598391</a>
</p>

<h3>AngularJS 20min</h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/DSC06699.jpg" alt="DSC06699" width="1280" height="853" class="alignnone size-full wp-image-2035" />

@naoya_itoさんによるAngularJSの入門講座。おなじみの軽妙語り口でAngularJSを始める際に理解するべきポイントや注意点を紹介していました。個人的に印象に残ったのは下記の点。

<ul>
<li>最初のサンプルがモンハンのスキルシミュレーターｗ <a href="https://github.com/naoya/mh4sim" target="_blank">https://github.com/naoya/mh4sim</a></li>
<li>「お前らのMVCは間違ってるなんて言ってないでコード書けよ = MVW」</li>
<li>双方向バインディングでリアルタイムにHTMLを更新</li>
<li>DOM操作はしないという制約によりマークアップの変更の影響を受けない！</li>
<li>引数を勝手に変えると動かないよ(文字列的にAngularが扱うので)</li>
</ul>

<script async class="speakerdeck-embed" data-id="4a73f2603e5d0131084906af3ff5da10" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

<h3>OnsenUIについて ~Angular.js+Topcoat~</h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/DSC06726-1024x682.jpg" alt="DSC06726" width="1024" height="682" class="alignnone size-large wp-image-2040" />

アシアルのお二人からはMonacaでも使われているOnsen UIにとても講演。Monaca自体はPhoneGapを利用したプロダクトですが、それと同様にAngularJSとTopcoatを活用して新しいコンポーネントを開発しているという意欲的な事例です。
OnsenUIについては公式サイトのドキュメント内で実際のデモを見ることもできます。
Reveal.jsを使ったスライドはスライド内でも実際のアプリが動いていてインパクトがあります。下記のIFRAME内でも動いていますので試してみてください。アプリがあるスライドで下向きの三角を押すとデモが始まります。

<a href="http://monaca.github.io/slides/2013-ng-jp/index.html#/" target="_blank">http://monaca.github.io/slides/2013-ng-jp/index.html</a>
<iframe src="http://monaca.github.io/slides/2013-ng-jp/index.html#/" width="100%" height="430"></iframe>

Home | Onsen UI
<a href="http://docs.monaca.mobi/onsen/ja/" target="_blank">http://docs.monaca.mobi/onsen/ja/</a>

WebAudioを利用したデモなどはとてもパワフルで印象的でした。今後はGUIで開発できるBuilderの開発を予定しているという事でコードを触らずにAngularJSの利点が活用できるようになりそうです。

<h3>AngularJS を実サービスで使ってみて</h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/DSC06736-1024x682.jpg" alt="DSC06736" width="1024" height="682" class="alignnone size-large wp-image-2044" />
@sakatamさんによる実案件での採用事例の紹介。GILTでユーザー側にAngularを採用した話。すぐに開発を進めるのでなく評価や学習の期間をしっかりととっていた点が注目を集めていたように思います。

<script async class="speakerdeck-embed" data-id="8915a1603e3f0131482c4e52bac46bd2" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

<h3>Angularでよくある質問とその回答</h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/DSC06765-1024x682.jpg" alt="DSC06765" width="1024" height="682" class="alignnone size-large wp-image-2057" />
ほぼフリーディスカッション形式に移行したセッション。悩んだ際に直接開発者に聞けるといううらやましすぎる境遇とエピソードがとても印象的です。

<a href="https://docs.google.com/presentation/d/1TMXfovfEioWD570EmLXobncV5tR96zgZd70DfFn2BVo/pub?start=false&amp;loop=false&amp;delayms=3000#slide=id.p"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/あなたの知りたかったAngularJS_-_Google_ドライブ-2-1024x720.png" alt="あなたの知りたかったAngularJS_-_Google_ドライブ-2" width="1024" height="720" class="alignnone size-large wp-image-2066" /></a>

<h3>LT:PHPとAngularの!ポンキーな関係</h3>
<script async class="speakerdeck-embed" data-id="10cd06a03ed30131bf09467a3fdfc5a9" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>
こちらはPHPでのAngularJSの実装例としてCakePHPとLithiumの２例を紹介しました。比較した中で特に強調したかったのは下記の点です。時間が不足していたので、同様のネタでまたどこかで話そうと思います。

<ul>
<li>PHPとJavaScriptを合成したスクリプトはレガシーコード化する。(ポンキー)</li>
<li>CakePHPの例: <a href="https://github.com/yandod/angularjs-cakephp-sample" target="_blank">https://github.com/yandod/angularjs-cakephp-sample</a></li>
<li>Lithiumの例: <a href="https://github.com/nateabele/li3-angular-presentation" target="_blank">https://github.com/nateabele/li3-angular-presentation</a></li>
<li>バックエンドはRESTを実装、フロントエンドは$resoucesを使うことでコード量が削減できる</li>
<li>この記事もおすすめです。 <a href="http://www.engineyard.co.jp/blog/2013/resource-oriented-webapp/">リソース指向のWebアプリ 〜Nate Abele氏 来日講演〜 | Engine Yard Blog JP</a></li>
</ul>

<h3>動画</h3>
HD版への切り替えや再生速度(1.5倍　２倍速など)の変更が可能です！

<strong>AngularJS 20min, OnsenUIについて ~Angular.js+Topcoat~</strong>
<iframe width="853" height="480" src="//www.youtube.com/embed/ZehPqvoUEYk" frameborder="0" allowfullscreen></iframe>


<strong>AngularJS を実サービスで使ってみて, Angularでよくある質問とその回答</strong>
<iframe width="853" height="480" src="//www.youtube.com/embed/1isSFQyUQVc" frameborder="0" allowfullscreen></iframe>

<strong>LT</strong>
<iframe width="853" height="480" src="//www.youtube.com/embed/s7zSWXjNa04" frameborder="0" allowfullscreen></iframe>

<strong>[PR] Engine YardのPaaSを利用すればクラウドの運用を強力にサポート。AngularJSを使ったインタフェースもあります。</strong>
<div><a href="http://ey.io/noyakshave"><img class="alignnone size-full wp-image-1889" style="border: 1px solid black;" alt="noyakshave_seminar_small" src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png" /></a></div>
