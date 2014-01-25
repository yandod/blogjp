---
layout: post
status: publish
published: true
title: Engine Yard Cloudのエンジニア向けご紹介
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 44
wordpress_url: http://www.engineyard.co.jp/blog/?p=44
date: 2012-10-15 05:44:08.000000000 +09:00
categories:
- Uncategorized
tags:
- 技術情報
- トライアル
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/EY3.Trdmrk.rgb_Hrzntl2.TM_.png"><img class="alignnone size-full wp-image-45" title="EY3.Trdmrk.rgb_Hrzntl2.TM" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/EY3.Trdmrk.rgb_Hrzntl2.TM_.png" alt="" width="302" height="165" /></a>

2012年10月1日より株式会社Engine Yardに入社した安藤です。前職まではPHPを使ったWebアプリケーションの開発や運用を主に行って来ましたが、当社においてはEngine Yardが提供するサービスや製品についてご紹介や開発者のサポートなどを行わせて頂く予定です。今回は実際のサービスの技術的な特徴や無料トライアルの利用方法についての情報をご紹介します。
<h2>Engine Yard Cloudの技術的特徴</h2>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/ey-regions_sm.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/ey-regions_sm.png" alt="" title="ey-regions_sm" width="500" height="280" class="alignnone size-full wp-image-71" /></a>
<ul>
	<li><strong>クリックするだけでアプリケーションが動作するサーバを作成</strong>
通常のVPSなどOSインストール直後の状態から実際にアプリケーションを動作させるには様々なソフトウェアの導入や設定が必要です。Engine Yard CloudではダッシュボードからクリックするだけでAmazon EC2上にインスタンスを作成し、各種設定を自動的に行いアプリケーションが動作する状態のサーバが稼働します。またWebサーバやデータベースサーバの分離、クラスタリング構成などバリエーションのある設定も同様にダッシュボードから設定できます。標準的な構成のRuby on Railsアプリケーションであれば設定ファイルなども自動的に設定されスムーズなデプロイが実現できます。各種パッケージのアップデート等もダッシュボード上からのクリックで行えます。</li>
	<li><strong>日本を含むAmazon EC2の提供リージョンに配置可能</strong>
作成されたサーバインスタンスは他の利用者と共有する事なく専有して利用できます。<a href="https://support.cloud.engineyard.com/entries/21010017" target="_blank">インスタンスが稼働するリージョン</a>もダッシュボード上で選択でき、日本やシンガポールなどのアジア地域にインスタンスを配置し日本からのアクセスに遅延なく応答できます。</li>
	<li><strong>インスタンスに対する様々なカスタマイズ</strong>
アプリケーションをすぐに動作させる事ができる反面、PaaSにはさまざまな制限が付く場合があります。Engine Yard Cloudの場合はダッシュボードからUnixパッケージの追加やChefのレシピを用いる事でサーバに更なる追加ソフトウェアの導入や設定ができます。公式にサポートされている言語はRuby、Node.jsが中心になっていますが今後はその他の開発言語を使ったアプリケーションの動作が可能になるでしょう。</li>
</ul>
<h2>無料トライアルの流れ</h2>
各種登録画面やインターフェースは英語のみとなっていますが、無料のトライアルアカウントは<strong>クレジットカードの登録は不要</strong>で誰でも自由に作成して頂けます。無料トライアルは500時間となっていますが、<strong>インスタンスを停止中は時間のカウントは行われません</strong>ので検証等であれば作業中のみに起動する事で500時間の中でもさまざまな検証や開発を行えるでしょう。(IPアドレスを削除するとなお万全です。)具体的なトライアルの手順については私の個人ブログにまとめて有りますのでご参考になさってください。
<ul>
	<li><a href="http://blog.candycane.jp/archives/1619">Engine Yard Cloudの無料トライアルでアプリをデプロイするまでの流れ : candycane development blog</a></li>
	<li><a href="http://blog.candycane.jp/archives/1670">Engine Yard Cloudでインスタンスを日本に置く＆sshでの接続を試す : candycane development blog</a></li>
</ul>
現在の所、日本の開発者の方でEngine Yard Cloudを触っている方はあまり多く無いのが現状です。無料のトライアルなどを通じてノウハウやご要望などを日本語で目にする事が出来るようになればと思います。今後は勉強会やセミナーの開催、ブログでのTIPSの紹介などを行なっていければと思います。ご要望やご質問がありましたらお気軽にお問い合わせください。
