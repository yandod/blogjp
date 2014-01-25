---
layout: post
status: publish
published: true
title: nanapi勉強会でVagrant + Berkshelfについて発表しました
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1847
wordpress_url: http://www.engineyard.co.jp/blog/?p=1847
date: 2013-11-13 12:31:57.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://atnd.org/events/44983" target="_blank">第1回 nanapi勉強会</a>にてVagrantとBerkshelfについて話してきました。今回のテーマは開発環境ということでVagrantの話は他の誰かがするのかなと思っていたのですが、誰もVagrantについて話さなかったので時間配分が難しかったです。

<h3>スライド</h3>
<script async class="speakerdeck-embed" data-id="a1da30602e370131c0c126e3fa07b66c" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

サンプルコード
<a href="https://github.com/yandod/omusubi">yandod/omusubi</a>
<a href="https://gist.github.com/yandod/7356902">Single file Vagrntfile which spin up Ubuntu 12.04 + PHP5.5 + Nginx + MySQL</a>

<h2>Vagrantはキャズムを越えた</h2>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/20131112_vagrant.009.png" alt="20131112_vagrant.009" width="1024" height="768" class="alignnone size-full wp-image-1853" />

開発環境としてVagrantを使うというスタイルは2013年で急速に市民権を得たようです。今回の参加者の中でも<strong>Vagrantを使っている人が半数を超えていた</strong>のでこの点については是非使いましょうという事になります。ただ仮想マシンの部分についてはVirtual Boxは手軽でいいのですがパフォーマンスが高くはないのでLXCなどの別のプラットフォームを使うという話も増えてきているように思います。わりとよく質問される所も含めて、これから使う人向けの注意点は下記のようなところです。

<ul>
<li>Vagrant 1.2以降はRubyを内蔵しているので<code>gem install vagrant</code>はしない</li>
<li>boxファイルをDropBoxで公開すると通信量の制限にかかって<del datetime="2013-11-13T07:11:14+00:00">アカウントが</del>リンクがロックされるので要注意</li>
<li>Vagrantで起動したインスタンスを運用環境にしない。(コマンド一つで破棄できる)</li>
<li>Windows環境ではいまのところ<code>vagrant ssh</code>は出来ず、自分でsshする。</li>
</ul>

<h2>Berkshelfを使うとシンプルで高機能</h2>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/20131112_vagrant.041.png" alt="20131112_vagrant.041" width="1024" height="768" class="alignnone size-full wp-image-1854" />

VMの設定部分はなんだかんだいってシェルスクリプトやAnsibleなどのワンタイムの構築をしている人が多いように思います。この理由がChef-Soloを使う場合はVagrantfileと一緒にCookbookを記述したり配布するのがめんどくさいという所だと思います。実際、これまでChef-Soloを使うVagrantfileを色々と書きましたがレシピの同梱や更新については大分手間を感じてきました。この問題をうまく解決してくれるのがBerkshelfです。Berkshelfは名前は知られているものの、まだ敬遠している人も多い気がしており、今回はBerkshelfをプッシュします。その理由は下記の通りです。

<ul>
<li>Berksfileを元に必要なクックブックを自動的に集める</li>
<li><strong>コミュニティクックブック以外にも対応</strong></li>
<li>プライベートgit、Chef Server、ローカルファイルなどのあらゆる方法でクックブックを取得できる</li>
<li>Vagrant Berkshelfプラグインを使えばberksコマンドなどを意識する必要もなし</li>
</ul>

個人的にも先入観があったのが、Berkshelfはコミュニティクックブックをインストールするツールなのではという誤解です。クックブックを自前で書いた方が楽なのではという風に考えると、自然と選択肢から外れてしまっていたのですが、実際は自作の非公開クックブックを集める事もできるのでgit submoduleなどをする必要は無くなります。
またこれにより自前のクックブックだけで解消が難しかった開発版のAPTサーバーの有効化などのコミュニティクックブックを気軽に使えるようになりました。例えば下記の例だと自前で書いた<code>omusubi</code>クックブックが取得するパッケージをコミュニティクックブックで開発版に変更しています。

<pre lang="ruby">
cookbook 'apt'
cookbook 'php5_ppa'
cookbook 'omusubi', git: "https://github.com/yandod/omusubi.git"
</pre>

Berkshelfを利用する事でクックブックの管理を簡単にするだけでなく、複雑なクックブックを書かないで部分的にコミュニティクックブックを使う事も簡単になります。Vagrantを使っていてクックブックの管理が面倒だと感じている方にはぜひともBerkshelf(ないしは類似ツールのLibrarian)の利用を強くお奨めします。

<hr>
<h4>Engine YardはChefに標準対応。AWS/Azureに両対応したPaaS</h4>
Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。PHPを利用したアプリケーションをデプロイする際は、Engine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>
