---
layout: post
status: publish
published: true
title: 'SendGrid Nightを開催しました (動画＆資料) #eytokyo'
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1729
wordpress_url: http://www.engineyard.co.jp/blog/?p=1729
date: 2013-10-23 18:26:49.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/10/DSC05542.jpg" alt="DSC05542" width="1280" height="853" class="alignnone size-full wp-image-1730" />

SendGrid Night - ey-tokyo | Doorkeeper
<a href="http://eytokyo.doorkeeper.jp/events/6569">http://eytokyo.doorkeeper.jp/events/6569</a>

Engine Yardのアドオンとしても多くの方にご利用頂いているメール送信サービス、SendGridのイベントを開催しました。
今回はSendGridの6番目の社員であるKen Appleさんを招きSendGridの歴史や現状、事例のLTといった一夜にしてSendGridが分かる内容のイベントでした。
今後もPaaSに関する様々な技術についてのイベントを開催する予定です。最新の情報は<a href="https://www.facebook.com/eyjapan" target="_blank">フェイスブックページ</a>のフォローをして頂ければと思います。


<h3>SendGrid入門</h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/10/DSC05532.jpg" alt="DSC05532" width="1280" height="853" class="alignnone size-full wp-image-1733" />

<script async class="speakerdeck-embed" data-id="be4a79701e1d0131f03e7e1022f85296" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

構造計画研究所の中井さんはKenさんとコンビを組む形でSendGridの基本を解説してくれました。日本での代理店業務を開始したという事でこれから本格的に日本向けのサービスでも使っていけるようになる事や、<strong>実は受信もできる</strong>といった機能面など重要なトピックの多い講演でした。講演の中でつぶやかれたツイートを見るとその様子がわかります。

https://twitter.com/maroon1st/status/392598751312748545

https://twitter.com/flect_jp/status/392600538119811072

https://twitter.com/snicker_jp/status/392602082198306816

https://twitter.com/maroon1st/status/392603936697241601

<h3>LT:SendGrid on Job-Hub</h3>
<iframe src="http://www.slideshare.net/slideshow/embed_code/27442652" width="512" height="421" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/oakbow/send-grind-on-job-hub" title="SendGrid on Job-Hub" target="_blank">SendGrid on Job-Hub</a> </strong> from <strong><a href="http://www.slideshare.net/oakbow" target="_blank">Hideki Ohkubo</a></strong> </div>

LTの一番手はJob-Hubについての大久保さんの発表です。忘れがちな設定などを実践的に解説しつつ、「トラブルがなさすぎて存在感が無い」という事で順調な利用をアピールしてくれました。またメールがバウンスした場合の取り扱いなどについては、会場にいる中井さんなどが迅速にフォローし疑問点が解消されたのも印象的です。

https://twitter.com/nakansuke/status/392610711165100032

<h3>LT:SendGrid Parse APIをデモってみる</h3>
<iframe src="http://www.slideshare.net/slideshow/embed_code/27456411" width="512" height="421" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/awwa500/send-grid-parse-api" title="SendGrid Parse APIをデモってみる" target="_blank">SendGrid Parse APIをデモってみる</a> </strong> from <strong><a href="http://www.slideshare.net/awwa500" target="_blank">Wataru Sato</a></strong> </div>

どうせLTをするならデモということで、Parse APIについての動作を披露して頂きました。実際の動作の様子や原理などは資料と動画をご覧になってみて下さい。

https://twitter.com/RyujiAMANO/status/392610815330639872


<h3>LT:SendGrid利用事例の紹介</h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/10/DSC05586.jpg" alt="DSC05586" width="1280" height="853" class="alignnone size-full wp-image-1738" />

フレクトの若葉さんからは実際の利用シーンや業務フローなどについても言及しながら利用事例をお話いただきました。

https://twitter.com/flect_jp/status/392616010420736001

<h3>LT:WantedlyがまだSendGridを使いこなしてない話</h3>
<iframe src="http://www.slideshare.net/slideshow/embed_code/27454646" width="512" height="421" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/yoshinorikawasaki/sendgrid-night-2013publish" title="WantedlyがまだSendGridを使いこなしてない話" target="_blank">WantedlyがまだSendGridを使いこなしてない話</a> </strong> from <strong><a href="http://www.slideshare.net/yoshinorikawasaki" target="_blank">Yoshinori Kawasaki</a></strong> </div>

先週のNew Relic Nightから引き続きの登板となる川崎さんからは「日本で一番SendGridを使っていると思われるWantedly」の事例をお話頂きました。
動かすだけなら本当にActionMailerの設定をするだけですが、信頼性を上げる為の設定を行う事を促された例など、SendGridを使う人なら誰にでも参考になる事例でした。

<h3>動画</h3>
<iframe width="640" height="480" src="//www.youtube.com/embed/oWN5Sexwk70" frameborder="0" allowfullscreen></iframe>

<strong>※動画の画質、再生速度の変更が可能です。</strong>

<table>
<tr>
<th>再生時間</th>
<th>タイトル</th>
</tr>
<tr>
<td>0:00</td>
<td>「SendGrid入門」 @nakansuke &amp; Ken Apple</td>
</tr>
<tr>
<td>29:45</td>
<td>「SendGrid on Job-Hub」大久保英樹</td>
</tr>
<tr>
<td>49:20</td>
<td>「SendGrid利用事例の紹介」　株式会社フレクト　若葉良介</td>
</tr>
<tr>
<td>1:03:25</td>
<td>「WantedlyがまだSendGridを使いこなしてない話」 @kawasy</td>
</tr>
</table>

その他の記事
<a href="http://nakansuke.hatenablog.com/entry/2013/10/25/002510">SendGrid Nightやりました - nakansukeのブログ</a>
<a href="http://snickerjp.blogspot.jp/2013/10/sendgrid-night_24.html">「SendGrid Night」に行ってきました！ : 元うなぎ屋</a>
<a href="http://blog.flect.co.jp/labo/2013/10/sendgrid-night-60eb.html">SendGrid Nightに行ってきた - フレクトのR&amp;Dブログ</a>

<hr>
Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。PHPを利用したアプリケーションをデプロイする際は、Engine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/trial"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>
