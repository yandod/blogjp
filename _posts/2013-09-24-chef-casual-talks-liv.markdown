---
layout: post
status: publish
published: true
title: Chef Casual Talksを生放送形式にして開催しました
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1490
wordpress_url: http://www.engineyard.co.jp/blog/?p=1490
date: 2013-09-24 12:31:33.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/Chef_Casual_Talks__Food_Fight_Japan__-_YouTube-2.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/Chef_Casual_Talks__Food_Fight_Japan__-_YouTube-2.png" alt="Chef_Casual_Talks__Food_Fight_Japan__-_YouTube-2" width="869" height="574" class="alignnone size-full wp-image-1491" /></a>

全員がスピーカーという形式で開催してきたChef Casual Talksですが、関西方面での盛り上がりも受けて生放送中心の形式で開催をしてみました。スライドも大変見やすく、発表中に質問も出やすいので今後もこの形式で開催できればと思います。

<iframe width="640" height="360" src="//www.youtube.com/embed/Moi6P4a_wVs" frameborder="0" allowfullscreen></iframe>

本編は 24:00 くらいからです。
29:04  「Windows Azure with Engine Yard Azureに対応したChefベースのPaaS」 @yando
51:35  「はかどるChefの小ネタ集」 @sawanoboly
1:29:27 「ほぼ質問でーす」

発表に使った資料は枚数もあまりないので、直接画像で張っておきます。

<h3>Engine YardのChef活用</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/Azure-with-Engine-Yard.005.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/Azure-with-Engine-Yard.005.png" alt="Azure with Engine Yard.005" width="720" height="540" class="alignnone size-full wp-image-1495" /></a>

７月から提供を開始したWindows Azure向けのPaaSが加わったことで３つのプラットフォーム向けの環境をChefで構築しクックブックのメンテナンスを行っています。OpsCodeを除くとこれだけ大々的にクックブックをメンテナンスし提供している企業は稀ではないでしょうか。

<h3>スタック構成</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/Azure-with-Engine-Yard.006.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/Azure-with-Engine-Yard.006.png" alt="Azure with Engine Yard.006" width="720" height="540" class="alignnone size-full wp-image-1496" /></a>
各プラットフォームはベースになるOSやChefのバージョンが異なっており、クックブックもブランチなどではなく別の系統として管理しています。クックブックを長年メンテナンスするとバージョンアップを行う事による書式や機能の変化をどのように取り扱うかというのは悩みの種になるかと思います。Engine Yardでは各プラットフォーム向け製品を提供するタイミングなどでこのバージョンを検討し、既存の環境はそのまま使えるようにした上で新しい基盤を作っています。

<h3>関連ツール</h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/Azure-with-Engine-Yard.007.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/Azure-with-Engine-Yard.007.png" alt="Azure with Engine Yard.007" width="720" height="540" class="alignnone size-full wp-image-1497" /></a>
Chefと併せて利用されるツールについても随時導入を進めています。クックブックに対してはfoodcriticとtravis ciを使った継続的インテグレーションを実施し、コールバックを利用して社内のツールと統合しています。また外部の枯れたクックブックを取り込むのにberkshelfも使っていますが、メインになるような複雑なクックブックについては引き続き、自前でのメンテナンスを行っています。


今年の上半期の話題をさらったChefですが、最近は話題の中心がserverspecなどを使ったテストやVagrantに移った印象があります。とはいえクックブックも記述やメンテナンスにはまだまだ奥が深い点がありますし、関連ツールのトレンドや本体のアップデートなどを適宜キャッチアップしていければと思います。

出演や観覧をしてみたい方は関西、東京どちらからでも構いません。また新たな中継地が増えるのも面白いと思いますのでわれこそはという方はぜひご連絡ください。

<a href="http://opsrock.in/2013/09/23/752">第２回 Chef Casual Talks Kansai開催レポート | Opsrock｜AWS OpsWorks, Opscode Chef を使用した自動化システムインテグレーション</a>

