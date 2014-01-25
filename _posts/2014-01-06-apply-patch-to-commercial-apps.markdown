---
layout: post
status: publish
published: true
title: 商用アプリケーションにおけるパッチ適用
author: 今中 崇泰
author_login: timanaka
author_email: timanaka@engineyard.com
wordpress_id: 2159
wordpress_url: http://www.engineyard.co.jp/blog/?p=2159
date: 2014-01-06 10:19:35.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<h3></h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/patch_top_image.png"><img class="alignnone size-large wp-image-1935" style="border: 1px solid black;" alt="Patch" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/patch_top_image.png" /></a>
<h3>商用アプリケーションにおけるパッチ適用</h3>
安定稼働しているアプリケーションシステムに対して、パッチを適用することほど億劫な作業はない、と思ったことのある保守・運用の担当者の方は多いのではないでしょうか。

私はERP/CRMパッケージを開発・販売する米国のベンダーの立場として、パッケージ導入に10数年にわたってお客様やビジネスパートナーを支援してきましたが、安定稼働しているシステムへのパッチ適用はまったく歓迎されるものではありませんでした。特にイントラネットでの利用が多いERPをご利用のお客様は、その傾向が強かったと言えます。

そのような状況を知りつつも、以下のような種類のパッチをお客様に提供し、それらの適用を促し続けていました。
<ul>
	<li>セキュリティアップデートパッチ (四半期に一度)</li>
	<li>法改正用メンテナンスパッチ (半年に一度)</li>
	<li>不具合修正のメンテナンスパッチ (随時)</li>
	<li>アップグレードパッチ (随時)</li>
</ul>
それは、パッチ適用を行っていただかなくては、不具合による障害や(たとえイントラネットのERPであったとしても)セキュリティの脆弱性によってサイバー攻撃の標的になりかねないことが理由としてあります。しかしそれだけではなく、パッチ適用をしないことで製品のアップグレードが保証されなくなり、保守費用をベンダーに支払っても、正規の技術サポートが受けられなくなる、もしくはサポートの範囲が限られるなどのベンダー都合の制約につながるためです。

オンプレミス形態のERP/CRMシステムの場合、OS層、ミドルウェア層(DBサーバー、APサーバー、開発ツール)、ランタイム層、アプリケーション層(共通基盤、会計、製造、人事など)といった、ありとあらゆるレイヤーへのパッチ適用が必要でその数も膨大になるため、どのレイヤーにどのレベルまでパッチを適用するかを、パッチ適用実施の半年前に定めるプロジェクトもある程です。それほどまでに骨の折れる大変な保守作業です。

そういう意味で、SaaS形態のアプリケーションを採用する利用者の視点に立てば、すべてのレイヤーのパッチ適用をSaaSベンダーに完全に委任できる画期的なソリューションであると言えるでしょう。

そしてまた、SaaS形態でアプリケーションを提供する先進的なアプリケーション開発ベンダーの視点に立てば、主なPaaSでアプリケーションを稼働させることで、プラットフォーム層(OS層、ミドルウェア層、ランタイム層)までのパッチ適用の保守作業をPaaSベンダーに委任でき、アプリケーションの継続的な開発保守に専念できるという大きなメリットを享受できます。

&nbsp;
<h3>PaaSを用いた場合のパッチ適用</h3>
主なPaaSベンダーは、OS層、ミドルウェア層(DBサーバー、APサーバー、開発ツール)、ランタイム層における保守運用サービスを提供しています。つまり、そのレイヤーに対する各種パッチの検証はPaaSベンダー側で予め行い、それらのパッチ適用までベンダーで行うか、もしくは容易に適用できる仕組みを提供するかのいずれかに分かれます。

PaaSと称するサービスベンダーの中には、仮想マシンのプロビジョニングとアプリケーションのデプロイの仕組みを提供しつつも、プラットフォーム層に対するパッチ適用、もしくはそれを支援する仕組みの提供まで行っていないものもあります。そのようなPaaSは、本当の意味でPaaSとは言えないでしょう。

ここでは本当の意味でPaaSと言えるサービスにフォーカスを置いて話しを続けます。

一般的に「<strong>パッチ適用までベンダーで行う形態</strong>」は「<strong>マルチテナント PaaS</strong>」を提供しているPaaSベンダーとされます。それに対して「<strong>パッチ適用を簡易的に行う仕組みを提供する形態</strong>」は「<strong>シングルテナント PaaS</strong>」を提供しているPaaSベンダーとされています。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Single_vs_Multi_for_PaaS.png"><img class="alignnone size-large wp-image-1794" alt="Single_vs_Multi_for_PaaS" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Single_vs_Multi_for_PaaS-1024x555.png" width="1024" height="555" /></a>

※「<strong>シングルテナント PaaS</strong>」と「<strong>マルチテナント PaaS</strong>」の優位性については、ブログ記事「<strong><a title="PaaSレイヤーの「シングルテナント」と「マルチテナント」はどちらが優位か？" href="http://www.engineyard.co.jp/blog/2013/singletenancy-vs-mutitenancy/" target="_blank">PaaSレイヤーの「シングルテナント」と「マルチテナント」はどちらが優位か？</a></strong>」をご参照ください。

ではここで、パッチ適用という観点で「<strong>シングルテナント PaaS</strong>」と「<strong>マルチテナント PaaS</strong>」の長所と短所をご紹介します。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/Single_vs_Multi_comptable_for_patch.png"><img class="alignnone size-large wp-image-1794" alt="Single_vs_Multi_for_PaaS" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/Single_vs_Multi_comptable_for_patch.png" /></a>

ブログ記事「<strong><a title="PaaSレイヤーの「シングルテナント」と「マルチテナント」はどちらが優位か？" href="http://www.engineyard.co.jp/blog/2013/singletenancy-vs-mutitenancy/" target="_blank">PaaSレイヤーの「シングルテナント」と「マルチテナント」はどちらが優位か？</a></strong>」でご紹介しているとおり、Engine Yardは「<strong>シングルテナント PaaS</strong>」を提供するベンダーであり、われわれのお客様が『<strong>Engine Yardは商用で利用するのに適しているPaaSである</strong>』と評価してくださる理由がこの表に込められています。

商用のアプリケーションに対するパッチ適用のタイミングは、PaaSベンダーにコントロールされるべきものではありません。プラットフォーム層のパッチを適用することによって、動作していたアプリケーションに障害が起きては、お客様のビジネスの大きな機会損失にも繋がりかねないためです。

そこでEngine Yardでは、パッチ適用のベストプラクティスとして、クローン環境を構築する機能と組み合わせて、以下の手順を定めています。

<strong>パッチ適用のベストプラックティス：</strong>
<ol>
	<li>クローン環境を構築する</li>
	<li>クローン環境にパッチ適用を行う</li>
	<li>クローン環境でアプリケーションの検証を行い、障害が発生しないことを確認する</li>
	<li>本番環境をアップグレードする</li>
	<li>クローン環境を停止して削除する</li>
</ol>
ステップ3のパッチ適用後の動作検証については、お客様ご自身で行っていただく必要がありますが、ステップ1、2、4、5については、簡単に実施できる仕組みを提供しています。

※ クローン環境の構築に関しては、ブログ記事「<strong><a title="アプリケーション環境のクローン機能" href="http://www.engineyard.co.jp/blog/2013/application-clone/" target="_blank">アプリケーション環境のクローン機能</a></strong>」をご参照ください。

&nbsp;
<h3>Engine Yardのパッチ適用</h3>
Engine Yard Cloudでは、ダッシュボードと呼ばれるGUIの画面から次の手順で簡単にパッチ適用を行うことができます。
<ol>
	<li><strong>パッチ適用が必要であることを確認</strong>
Engine Yard Cloudのアプリケーション環境の詳細ページに表示される「<strong>Upgrade</strong>」ボタンが青くなり「<strong>▲</strong>」マークが表示されている場合、パッチ適用が必要であることを意味します。<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/upgrade_button_clone.png"><img class="alignnone size-full wp-image-1943" style="border: 1px solid black;" alt="Patch_Apply_Step1" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/upgrade_button_clone.png" /></a></li><br>
	<li><strong>どのようなパッチを適用する必要があるかを確認</strong>
「<strong>Upgrade</strong>」ボタンをクリックすると、ご利用のアプリケーション環境に対して適用が必要なパッチがリストされます。<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/upgrade_items_list_clone.png"><img class="alignnone size-full wp-image-1943" style="border: 1px solid black;" alt="Patch_Apply_Step2" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/upgrade_items_list_clone.png" width="780" height="894" /></a></li><br>
	<li><strong>パッチ適用を実施</strong>
「<strong>Upgrade Environment</strong>」ボタンをクリックし、適用の完了を待ちます。<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/upgrade_items_clone.png"><img class="alignnone size-full wp-image-1943" style="border: 1px solid black;" alt="Patch_Apply_Step3" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/upgrade_items_clone.png" /></a><br><br>本番環境にパッチ適用を行う場合には、CLIを用いてメンテナンスモードに切り替えてから実施することをご検討ください。メンテナンスモードの切り替えコマンドについては、「<strong><a title="eyコマンドの基本" href="https://support.cloud.engineyard.com/entries/25068712?locale=67" target="_blank">eyコマンドの基本</a></strong>」をご参照ください。</li>
</ol>
なお、この機能で適用されるパッチとしては以下のような種類が含まれます。
<ul>
	<li>プラットフォームのバグ修正</li>
	<li>プラットフォームの新機能追加</li>
	<li>プラットフォームの既存コンポーネントのチューニング</li>
	<li>プラットフォームの既存コンポーネントのアップデート</li>
	<li>プラットフォームの既存コンポーネントのセキュリティ脆弱性</li>
	<li>プラットフォームの新規コンポーネントの追加</li>
	<li>新規の仮想インスタンス種類への追加対応</li>
	<li>アドオンとの連携設定の追加・修正
など</li>
</ul>
&nbsp;
<h3>参考情報</h3>
ここでは、本トピックに関連して参考になる情報のリンクをご紹介します。必要に応じて、ご覧いただければと思います。
<ul>
	<li><a title="PaaSレイヤーの「シングルテナント」と「マルチテナント」はどちらが優位か？" href="http://www.engineyard.co.jp/blog/2013/singletenancy-vs-mutitenancy/" target="_blank">PaaSレイヤーの「シングルテナント」と「マルチテナント」はどちらが優位か？</a></li>
	<li><a title="アプリケーション環境のクローン機能" href="http://www.engineyard.co.jp/blog/2013/application-clone/" target="_blank">アプリケーション環境のクローン機能</a></li>
	<li><a title="環境のアップグレード" href="https://support.cloud.engineyard.com/entries/22329867?locale=67" target="_blank">環境のアップグレード</a></li>
	<li><a title="eyコマンドの基本" href="https://support.cloud.engineyard.com/entries/25068712?locale=67" target="_blank">eyコマンドの基本</a></li>
	<li><a title="Upgrade an Environment (英語版)" href="https://support.cloud.engineyard.com/entries/21009922?locale=67" target="_blank">Upgrade an Environment (英語版)</a></li>
	<li><a title="Using Application Maintenance Pages (英語版)" href="https://support.cloud.engineyard.com/entries/21016428?locale=67" target="_blank"> Using Application Maintenance Pages (英語版)</a></li>
</ul>
&nbsp;
<div><a href="http://ey.io/noyakshave"><img class="alignnone size-full wp-image-1889" style="border: 1px solid black;" alt="noyakshave_seminar_small" src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png" /></a></div>
