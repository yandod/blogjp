---
layout: post
status: publish
published: true
title: クリックだけで出来るスケールアウトを無料で試す
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 374
wordpress_url: http://www.engineyard.co.jp/blog/?p=374
date: 2012-12-18 10:41:24.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/Getting_Start_EY_Cloud.key-1.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/Getting_Start_EY_Cloud.key-1.jpg" alt="" title="Getting_Start_EY_Cloud.key-1" width="534" height="338" class="alignnone size-full wp-image-376" /></a>

トラフィックの多いWebサービスなどにおいて、性能と信頼性を向上させる為に利用されるのがアプリケーション サーバーやデータベースのスレーブ サーバーを追加するスケールアウトのアプローチです。この方法を取ることでマスター データベースへの書き込み処理の限界を迎えるまでは単純にノードを追加するだけでシステムのキャパシティを増強できます。おそらく多くの方がこのような構成のシステムでの開発や運用を行ったことがあるのではないでしょうか。
こういったスケールアウトを抽象化して提供しているプラットフォームもありますが、Engine Yard CloudはEC2のインスタンスの追加を規準にした明快な方法でスケールアウトを提供しています。

<h2>無料トライアルでもスケールアウト</h2>
Engine Yard CloudではダッシュボードからEnvironmentという設定項目でアプリケーション・サーバーやデータベース サーバー、ユーティリティ サーバーなどのインスタンスの大きさや数を設定できます。ダッシュボードから設定した内容はインスタンスに自動で反映され、<span style="color:red"><strong>ロードバランサーへの登録やアプリケーションからデータベースへ接続する設定なども自動的に反映されます。</strong></span>従来、無料トライアル期間中は起動できるインスタンスが1台に限定されており、この機能が制限されていました。しかし今回、この制限が撤廃され<strong>無料トライアル期間中でもインスタンスの追加によるスケールアウト設定を利用できるようになりました。</strong>

<h2>設定の方法</h2>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/Engine-Yard-Cloud-—-Cluster-configurations.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/Engine-Yard-Cloud-—-Cluster-configurations.jpg" alt="" title="Engine Yard Cloud — Cluster configurations" width="639" height="658" class="alignnone size-full wp-image-387" /></a>

アプリケーションを稼働させる際のクラスタリングの構成などはリポジトリ名やランタイムなどを設定した次の画面に表示される上記のメニューから行います。<strong>シングルインスタンス</strong>(アプリケーション・サーバーとデータベースを同居)、<strong>ステージング</strong>(アプリケーション サーバー2台、データベース サーバー1台)、<strong>プロダクション</strong>(アプリケーション サーバー3台、データベース サーバー1台、スレーブデータベース サーバー1台)のようにプリセットされた設定と自由にサーバー構成を設定できるカスタム設定が選べます。プリセット設定に後からノードを追加する事も出来ますし、カスタム設定では任意の構成を数値を入力して作成できます。<strong>大量のインスタンスを数値を入力するだけで構成できますが、無料トライアル時間や請求はインスタンスの数だけ計上されるので注意が必要です。</strong>

<table>
<tr>
  <th>タイプ</th>
  <th>App</th>
  <th>DB</th>
  <th>Util</th>
  <th>合計</th>
<tr>
  <th>シングルインスタンス</th>
  <td colspan="2" align="center">1</td>
  <td>任意</td>
  <td>1</td>
</tr>
<tr>
  <th>ステージング</th>
  <td>2</td>
  <td>1</td>
  <td>任意</td>
  <td>3</td>
</tr>
<tr>
  <th>プロダクション</th>
  <td>3</td>
  <td>2</td>
  <td>任意</td>
  <td>5</td>
</tr>
<tr>
  <th>カスタム</th>
  <td>任意</td>
  <td>任意</td>
  <td>任意</td>
  <td>任意</td>
</tr>
</table>
<br/>

<h2>環境のクローンも可能</h2>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/Engine-Yard-Cloud-—-Environment-trial-of-application-todo.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/Engine-Yard-Cloud-—-Environment-trial-of-application-todo.jpg" alt="" title="Engine Yard Cloud — Environment trial of application todo" width="691" height="381" class="alignnone size-full wp-image-405" /></a>
ノードの追加だけではなく、環境のセットを丸ごとクローンする事もできます。この機能は本番環境をクローンしたステージング環境を作ってシステムのアップデートや最新のアプリケーションをテストするといった用途に最適です。テストや検証が終わればクローンしたステージング環境を破棄してしまいましょう。必要になればまた本番環境をクローンすれば良いわけですからね。

<h2>無料トライアルの500時間をうまく活用</h2>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/Engine-Yard-Cloud-—-Cluster-configurations-1.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/12/Engine-Yard-Cloud-—-Cluster-configurations-1.jpg" alt="" title="Engine Yard Cloud — Cluster configurations-1" width="536" height="437" class="alignnone size-full wp-image-393" /></a>
アプリケーション サーバーやデータベース サーバーへのノードの追加をダッシュボードから簡単に行う事ができ、設定なども自動的に変更できるというEngine Yard Cloudの利点は是非とも試して頂きたいと思います。無料トライアルはインスタンスの稼働時間合計が500時間までとなっています。複数のインスタンスを稼働させた場合はその数に応じた分で稼働時間がカウントされます。インスタンスは利用する際にだけ起動し、使い終わったら停止させるというのを守る事で無料トライアルの枠内でもさまざまな検証をして頂けるでしょう。

<h2>作りこまれた環境をすぐに稼働</h2>
イメージファイルなどを利用してすぐにインスタンスを起動できるIaaSプラットフォームは色々とありますが、Engine Yard Cloudのインスタンスはそれをさらにアプリケーションが稼働するように作りこまれているのが特徴です。ロードバランサーにはHAProxyかELBを使い、nginxやPassenger、unicornなどのミドルウェアを最適化して導入済みです。このようなノードで構成したクラスタ環境をクリックだけで構築できる事で従来インフラ作業に取られていた時間を開発に使って頂ければ幸いです。
