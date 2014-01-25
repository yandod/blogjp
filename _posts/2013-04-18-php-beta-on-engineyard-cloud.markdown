---
layout: post
status: publish
published: true
title: Engine Yard CloudでPHPを利用できるようになりました
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 889
wordpress_url: http://www.engineyard.co.jp/blog/?p=889
date: 2013-04-18 15:09:18.000000000 +09:00
categories:
- Uncategorized
tags: []
comments:
- id: 35
  author: Engine Yard Cloud上のPHPにDrupalをデプロイ - Engine Yard Blog JP | Engine Yard Blog
    JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/drupal-on-engine-yard/
  date: '2013-04-24 19:04:27 +0900'
  date_gmt: '2013-04-24 10:04:27 +0900'
  content: '[...] Engine Yard Cloud上でPHPが動作するようになった事をお知らせして以降、さっそくPHPのデプロイを試して頂いた方がDrupalを利用していました。今回、設定の手順やデプロイをスムーズにするスクリプトを書いたのでこれらを併せてDrupalを動作させる手順として記事にしようと思います。
    [...]'
- id: 39
  author: Engine Yard Cloud上のPHPにCandyCaneをデプロイ - Engine Yard Blog JP | Engine Yard
    Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/candycane-on-engineyard/
  date: '2013-04-26 17:00:07 +0900'
  date_gmt: '2013-04-26 08:00:07 +0900'
  content: '[...] Engine Yard Cloud上のPHPにDrupalをデプロイ Engine Yard CloudでPHPを利用できるようになりました
    [...]'
- id: 41
  author: Engine Yard で WordPress を動かす | dogmap.jp
  author_email: ''
  author_url: http://dogmap.jp/2013/05/02/wordpress-on-engine-yard/
  date: '2013-05-02 19:01:33 +0900'
  date_gmt: '2013-05-02 10:01:33 +0900'
  content: '[...] PHP が使えるように設定します。 Engine Yard CloudでPHPを利用できるようになりました &#8211; Engine
    Yard Blog JP | Engi... # ダッシュボードが一部日本語化されてるので「Tools」-「Early [...]'
---
お問い合わせ頂くことの多かったEngine Yard CloudでのPHPサポートを早期アクセス（ベータ版）として公開しました。これによりChefによるカスタマイズなどをせずにPHPのアプリケーションをEngine Yard Cloud上で実行できます。無料トライアルや料金、リージョンなどはRubyなどの他のスタックと全く同一です。PHPをご利用頂くにはログインした後の画面のヘッダーから早期アクセス(Early Access)のページを開きます。

<img alt="" src="https://lh6.googleusercontent.com/TCFyqz1zBXr8ezXxe0PHuur1FOSRsWr90_kOMliJnhJbkgFwFzLlmkny3drtD9mbwSd1omcGVTg66wimHEzhSDEDnDYcaRuaDKNeqiKF7tllh2o1SyO2SYYCJg" width="579px;" height="187px;">

ページ内をスクロールすると様々な早期アクセス機能の中のひとつとして「PHP」の項目がありますので、「Enable」をクリックしてPHPを有効化します。

<img alt="" src="https://lh3.googleusercontent.com/4FDRhpTH5AQm8yDppz_hRs229BoqHbMtd7LHcGsLNxSTENbiA_if5zakIkz9gN8-xukYTKQ-NcLdYOGKNpxFRe-nSZK2BVK93yt8Q4vx_dTs174lJOGSQtHsjg" width="564px;" height="174px;">

PHPを有効化するとアプリケーションの作成画面の「Application Language」からRuby、Node.jsと同じようにPHPが選択できるようになります。デプロイするアプリケーションについてはサンプルアプリケーションのリンクをクリックするか、ご利用になるリポジトリを指定します。またドキュメントルートになるディレクトリがあれば追加で指定を行います。

<img alt="" src="https://lh3.googleusercontent.com/gUWD9VW8G-k1O-oZDrtOIfkVPcPQ6Kip9Z5jJzlhbo5WVgT__GhEYrmnnSQVHWzeK7Ez-niAzQtMVTYTgYfJrMf90k_uWc6jG6gJY4dc9wjVuYYWL8jwoq-ZyQ" width="600px;" height="382px;">

実行エンジンについてはphp-fpmを利用した構成となります。データベースについては他のスタックと動揺にMySQL、PostgreSQL、データベース無しなどが選択できます。


<img alt="" src="https://lh6.googleusercontent.com/LXgMEev1KUWFpE0mD4arvAxiw9na_-3atBs-oKhGnqA5y4FYBc6-k1sHfn4W5QTHn9StRJ48Re8WtLFh1uu_1LyXrVFtMqYh2KYkPPUAfmF3Sxs-vzrGhrJCUA" width="576px;" height="564px;">

あとはデプロイを行うだけでアプリケーションが動作した状態となります。サンプルアプリケーションは<a href="https://github.com/engineyard/howto" target="_blank">こちらのリポジトリ</a>で公開されているものを利用しています。

<img alt="" src="https://lh4.googleusercontent.com/O_5XA4d9i7vvu1dMg3saXzniJmHOj7DJVaWbK8HqrLIIlDRgPt_AI8sy1zL9z2Lvw68F-Qdi2iEk3kCeebWMOli7Q7QLZM9OE30m90rjEtXNGSbvTvlQDF8z0g" width="546px;" height="184px;">

.htaccessによるrewriteを利用している場合や、データベースのマイグレーションを行う場合はSSHでの接続やデプロイフックの利用が必要になりますが、皆様からの要望に応じてさらなる機能がダッシュボードに追加されていく予定です。スケーラブルな環境を自動で運用できるEngine Yard CloudをPHPのアプリケーションで活用させるよい機会と思いますので是非無料トライアルをお試し頂き、フィードバックなどを頂ければと思います。宜しくお願い致します。


<div style="text-align:center"><span ><a href="http://www.engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" style="border:1px solid black"/></a></span></div>
