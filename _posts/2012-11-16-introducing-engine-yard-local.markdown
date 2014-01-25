---
layout: post
status: publish
published: true
title: Engine Yard Local のご紹介
author: Edward Chiu
author_login: edwardchiu
author_email: edwardchiu@engineyard.com
wordpress_id: 263
wordpress_url: http://www.engineyard.co.jp/blog/?p=263
date: 2012-11-16 16:09:37.000000000 +09:00
categories:
- Uncategorized
tags: []
comments:
- id: 27
  author: 「初めてのChefの教室」を開催しました。(動画&amp;資料) - Engine Yard Blog JP | Engine Yard Blog
    JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/engineyard-meetup-chef-seminar/
  date: '2013-02-25 12:41:27 +0900'
  date_gmt: '2013-02-25 03:41:27 +0900'
  content: '[...] Engine Yard Cloudにはクラウド上と同じインスタンスをローカル環境上に作成するEngine Yard Localというツールを公開しています。このツールは話題に上がったVagrantを使ってクラウド上と同じ環境を構築するという事でChefとVagrantを使った運用とクラウド環境を透過的に扱えるなかなかスグレモノのツールです。こちらについてはVagrant中心の勉強会を行う際にはご紹介できればよいなと思っています。
    [...]'
---
あなたはクライアント向けの6ヶ月に及ぶプロジェクトのラスト2回のスプリントを終えたところとしましょう。クライアントは2週間後の正式公開に向けてあなたのアプリケーションをクラウド環境に移してほしいと言っています。

開発にやり残しがないようにするだけでなく、アプリケーションをクラウドにデプロイし、なおかつ全ての機能がクラウドスタック上で動作する事を確認しなければならないでしょうか。そんな事はありません。

不安を感じる必要はありません。Engine Yard は Engine Yard Local というツールを開発しました。我々はコミュニティの開発者からの声を聞いてきました。それによるとローカル開発環境からプロダクション環境へ素早く移行できる仕組みが必要とされていました。

つまり、 Engine Yard Local はEngine Yard Cloud に近いインスタンスを使ってローカルなクラウド環境でアプリケーションの開発とテストを出来るようにします。

まず必要になるのはあなたのマシンに VirtualBox と Engine Yard Local が入っていることです。インストールが終わったら下記のコマンドをあなたのアプリケーションのトップディレクトリで実行します。これにより仮想マシンが起動し、 cookbook のレシピがインストールされ、オペレーティングシステムやWebサーバー、アプリケーションサーバー、ロードバランサーなどのコンポーネントが導入されます。

<div class="wp_syntax"><div class="code"><pre class="" style="font-family:monospace;">$ ey-local up</pre></div></div>

設定が終われば次のコマンドを実行できます。

<div class="wp_syntax"><div class="code"><pre class="" style="font-family:monospace;">$ ey-local status</pre></div></div>

<p><strong id="internal-source-marker_0.22513724328018725"><br />
</strong>画面上では仮想マシンが起動し実行されているのが確認できます。</p>
<p><strong id="internal-source-marker_0.22513724328018725"><br />
<img src="https://lh3.googleusercontent.com/VWacbYW9J98zda8mVp56_H_x0Dv97yx6Tq1Zp5zAcBinVQQvy4MJm-jPm44icjf6WONok2I1JLVELQ7jdIMexmtY6gQ4KEDQpMiPxdZOt2ul4AY0Vc0" alt="" width="615px;" height="244px;" /><br />
</strong><br />
仮想マシンが起動すれば、<a href="http://127.0.0.1:8080/">http://127.0.0.1:8080/</a> にアクセスすれば稼働するアプリケーションが見えるようになります。</p>
<p><strong id="internal-source-marker_0.22513724328018725"><br />
<img src="https://lh5.googleusercontent.com/1X8xWvMVMn2tO_dBFwydMj5JzaYu_j_tYlS1hQRFXmDP_MbtEi83t64pXoVdK1poTw7ns6VonDqI35_1g2ySq_0FC6CFxNHc8NKQOPLHxbpDdh76SUI" alt="" width="620px;" height="466px;" /></strong></p>

Engine Yard Local は Engine Yard のその他の環境と同じく SSH を通じてインスタンスを完全にコントロールできます。これによりプロダクション環境で Passenger のログを見るようにスタックを理解することができます。

<p><strong id="internal-source-marker_0.22513724328018725"><img src="https://lh3.googleusercontent.com/gQkS2-cYb2m7Yj1waN7shslpLxBfQu6iUZau_9dUfcAPtuELfDLJamAJd0jx45HoQ6iWSedfL7vVA9hK-TBg29LtPJBJW7EOMzG9ydvkwFvsaFQyNKU" alt="" width="619px;" height="316px;" /></strong></p>

ご覧のとおり Engine Yard Local はアカウントの作成、設定やアプリケーションのデプロイ、インスタンスへの課金を避ける優れた方法を提供します。Engine Yard Local により無制限で無料である事を除いてクラウド環境上であるとみなしてテストを行う事ができます。

<p>Engine Yard Local の詳細については<a href="http://www.engineyard.co.jp/products/local">http://www.engineyard.co.jp/products/local</a>をご覧ください。(訳注:日本語訳のドキュメントは現在準備中です。) 動画でご覧になりたい方は<a href="http://www.engineyard.com/video/53194083">スクリーンキャスト</a>をご覧ください。<strong id="internal-source-marker_0.22513724328018725"><br />
</strong><script type="text/javascript">AKPC_IDS += "13404,";</script></p>
