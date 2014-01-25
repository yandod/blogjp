---
layout: post
status: publish
published: true
title: 'New Relic Nightを開催しました。(動画＆スライド) #eytokyo'
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1690
wordpress_url: http://www.engineyard.co.jp/blog/?p=1690
date: 2013-10-18 17:39:10.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/10/DSC05403.jpg" alt="DSC05403" width="1280" height="853" class="alignnone size-full wp-image-1691" />

2013/10/17に弊社オフィスにてサーバー・アプリケーションの監視サービス、New Relicについての勉強会を開催しました。

<div class="note">
<strong>New Relic Night - ey-tokyo | Doorkeeper</strong>
<a href="http://eytokyo.doorkeeper.jp/events/6233">http://eytokyo.doorkeeper.jp/events/6233</a>
</div>

PaaSやAWS上でNew Relicを使っている方は非常に多いようですが、問題の解決方法などについて利用経験のある方で情報交換の機会にと思い企画しましたがとても素晴らしい内容になりました。

各講演の資料と動画をご紹介します。当日のツイートについても下記にまとめてあります。
<a href="http://togetter.com/li/578482">New Relic Night まとめ #eytokyo - Togetter</a>

その他の感想記事
<a href="http://blogaomu.com/2013/10/17/new-relic-night/">New Relic Night に参加してきた - Blogaomu</a>

<h2>New Relic入門 @yando</h2>
<iframe src="http://www.slideshare.net/slideshow/embed_code/27319113" width="597" height="486" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/yandod/new-relic-27319113" title="New relic" target="_blank">New relic</a> </strong> from <strong><a href="http://www.slideshare.net/yandod" target="_blank">yandod</a></strong> </div>

New Relicの基本的な所についての解説です。いくつかあやふやな点がありましたが、後続の講演でフォローしていただけましたので今回のイベントのトータルで見て頂くとより理解が深まるかと思います。ポイントは下記のような点です。

<ul>
<li>エージェントを導入するだけで監視元サーバ不要の監視</li>
<li>iOSアプリのプッシュ通知を使った監視や、見たことのない監視項目が利用可能</li>
<li>Engine Yardから利用するとスタンダード($48相当)が何台でも無料なので導入しないともったいない</li>
</ul>

従来型の監視システムでも時間と手間をかければ同じような監視は可能ですが、それがごく手軽に利用できるという点に大きな価値があるという点を特にお伝えしたかったです。おそらく社内で監視システムを構築する際に監視用のiOSアプリまで作りこむ事ができる余裕のある企業はほとんど存在しないといって良いと思います。

<h2>WantedlyとNew Relicとサイト高速化 @kawasy</h2>
<script async class="speakerdeck-embed" data-id="63916410194d0131674c7215726d6691" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

川崎さんからは<a href="https://www.wantedly.com/" target="_blank">Wantedly</a>での利用事例をお話頂きました。Real User Monitoringを使ったユーザーの体感速度を改善する為の活動は誰にとっても参考になる内容だったと思います。またHipChatとの連携など簡単な設定だけで便利になるという事の利点をわかりやすく説明して頂きました。

特に印象に残ったのは「レンダリング時間のレポートはユーザーの体感速度とは必ずしも一致しない。」「Time To First Byteなどの考え方も必要」といったチューニングを行う際の肌感覚の部分です。これは誰もが覚えておいて損は無い部分ではないでしょうぁ。

<h2>New Relic with PHP @hiro_y</h2>
<iframe src="http://www.slideshare.net/slideshow/embed_code/27288003" width="597" height="486" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/HiroyukiYamaoka/new-relic-night-27288003" title="New Relic with PHP" target="_blank">New Relic with PHP</a> </strong> from <strong><a href="http://www.slideshare.net/HiroyukiYamaoka" target="_blank">Hiroyuki Yamaoka</a></strong> </div>

山岡さんからは従来型の監視システムの利用経験も踏まえた上で、利点と欠点についてお話頂きました。またReal User Monitoringを有効にした際に出力されるJavaScriptの例を示して頂き、謎が一つ解けました。Engine Yard上で稼働している<a href="http://comap.at/">Comap</a>とAWSで稼働している別のサービスでもそれぞれNew Relicをお使いとの事です。


<h2>Idobata と New Relic の話 @ursm</h2>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/10/Idobata.jpg" alt="Idobata" width="1008" height="592" class="alignnone size-full wp-image-1702" />
浦嶌さんからは最近、注目の集まってきている開発者向けチャット、<a href="https://idobata.io/" target="_blank">idobata</a>での利用事例をお話頂きました。New Relicの統計項目で不満に感じた点を拡張する事で必要なデータの統計が見れるようにカスタマイズしていく事例は非常に貴重な内容でした。また講演で紹介していた競合サービスや統計の拡張のGemなどの情報も見逃せないポイントでした。

浦嶌さんの講演はスライドがありませんので、動画でご覧ください。<strong>New Relicで取得できなかった項目を実際にカスタマイズして取得した実績の紹介は貴重です。</strong>

講演で紹介していたGem
<a href="https://github.com/newrelic/rpm_contrib">newrelic/rpm_contrib</a>

<h2>ランサーズでの事例 秋好聡</h2>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/10/DSC05436.jpg" alt="DSC05436" width="1280" height="853" class="alignnone size-full wp-image-1705" />
秋好さんからはランサーズにNew Relicを導入してみたというお話を頂きました。たくさんあるアプリケーション・サーバーのうちまずは1台に導入してみて様子を見るというスタイルは既存システムへの導入を検討している方にはとても身近な内容だったのではと思います。

<h2>動画</h2>
<iframe width="640" height="480" src="//www.youtube.com/embed/7YeAdmMKjDM" frameborder="0" allowfullscreen></iframe>

※画質と再生速度の変更が可能です。

<table>
<tr>
<th>開始時間</th>
<th>内容</th>
</tr>
<tr>
<td>0:00</td>
<td>New Relic 入門 @yando</td>
</tr>
<tr>
<td>33:00</td>
<td>WantedlyとNew Relicとサイト高速化 @kawasy</td>
</tr>
<tr>
<td>43:20</td>
<td>New Relic with PHP @hiro_y</td>
</tr>
<tr>
<td>50:16</td>
<td>Idobata と New Relic の話 @ursm</td>
</tr>
<tr>
<td>1:03:06</td>
<td>ランサーズでの事例 秋好聡</td>
</tr>
</table>
<hr>
Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。PHPを利用したアプリケーションをデプロイする際は、Engine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/trial"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>
