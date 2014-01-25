---
layout: post
status: publish
published: true
title: アプリケーション環境のクローン機能
author: 今中 崇泰
author_login: timanaka
author_email: timanaka@engineyard.com
wordpress_id: 1907
wordpress_url: http://www.engineyard.co.jp/blog/?p=1907
date: 2013-11-25 13:56:44.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<h3></h3>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone.png"><img class="alignnone size-large wp-image-1935" alt="Clone" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone-1024x579.png" width="1024" height="579" /></a>
<h3>アプリケーションの開発・運用における複数の環境</h3>
商用アプリケーションであれば、導入企業の規模やアプリケーション機能数に関わらず、「本番環境」以外に「開発環境」や「ステージング環境」を準備して、アプリケーションの開発プロジェクトを進めていることでしょう。これは、アプリケーションの開発手法がアジャイルであっても、ウォーターフォールであっても言えることでもあります。

私が長年携わってきたERP/CRMパッケージを用いたウォーターフォール型のシステム構築においても、「単体テスト環境」、「結合テスト環境」、「総合テスト環境」、「検収テスト環境」、「本番環境」という多くの環境を用いてプロジェクトを進めてきました。

「<a title="The Twelve-Factor App" href="http://12factor.net" target="_blank"><strong>The Twelve-Factor App</strong></a>」の「<strong><a title="The Twelve-Factor App - X. Dev/prod parity" href="http://12factor.net/dev-prod-parity" target="_blank">X. Dev/prod parity</a></strong>」 によると、このような複数のアプリケーション環境は、「時間」、「人材」、「ツール」という3つの領域におけるギャップによって、徐々に格差が生まれてくるものであると言われています。
<ul>
	<li><strong>時間のギャップ：
</strong>開発者が開発したコードが本番環境に反映されるまでに、数日、数週間、場合によっては数ヶ月かかる。</li>
	<li><strong>人材のギャップ：
</strong>コードは開発者が書き、Opsエンジニアがそれをデプロイする。</li>
	<li><strong>ツールのギャップ：
</strong>開発者はNginx、SQLite、OS Xのようなスタックを利用し、デプロイ先の本番環境ではApache、MySQL、Linuxを利用することがある。</li>
</ul>
実際に、ローカルPCで開発して正常に動作することを確認したアプリケーションが、ひとたび開発環境にデプロイするとエラーが発生して、なかなか解決に至らないケース。その他に、開発環境で動作しているアプリケーションを、いざステージング環境や本番環境にデプロイするといつの間にかデータベースのオブジェクトの定義やデータ状態の違いが生じていることで動作しないケース。このような経験をされたことがあるアプリケーション開発者の方々は多いのではないでしょうか。

「<strong>ツールのギャップ</strong>」という観点で言うと、スタックの種類の違いだけでなく、環境によってスタックのパッチレベルの違いが発生することもよくあります。

「<strong>The Twelve-Factor App</strong>」では、継続的にデプロイしやすいよう、これら複数の環境のギャップを極小化し、それを維持することが重要であると解説が続けられています。
<ul>
	<li><strong>時間のギャップを極小化：
</strong>開発者が書いたコードを数時間後ないし数分後にはデプロイを行う。</li>
	<li><strong>人材のギャップを極小化：
</strong>コードの開発者は、書いたコードのデプロイに関わり、本番環境の挙動を監視する。</li>
	<li><strong>ツールのギャップを極小化：
</strong>開発環境と本番環境をできる限り一致させた状態を維持する。</li>
</ul>
さすがに、このガイドラインをあらゆる領域のシステム開発において採用することは難しいのは言うまでもありません。と言うのも、これは、Eコマースやモバイルアプリケーション、そしてSaaSモデルのアプリケーションなど、時流に合わせて継続的に開発を行うWebサービスに求められる要素として纏められているからです。

しかし、そうは言うものの、ERPなどの大規模なアプリケーション システム構築であったとしても、「<strong>The Twelve-Factor App</strong>」には非常に参考になる要素が含まれています。是非、参考にしてみてはいかがでしょうか。

&nbsp;
<h3>Engine Yardのクローン機能の特長</h3>
Engine Yardが提供しているPaaSでは、「時間」、「人材」、「ツール」の3つの領域におけるギャップを埋める機能が備わっています。それは、アプリケーション環境を容易に複製できる「クローン機能」で、以下のような特長があります。
<ul>
	<li><strong>必要な時にクローン環境を構築</strong>でき、<strong>不要になれば削除</strong>可能。</li>
	<li>クローン環境は<strong>クローン元の環境と同一のシステム構成</strong>で構築。</li>
	<li>クローン環境は<strong>クローン元の環境の最新のデータ状態</strong>で構築。</li>
	<li>クローン環境は<strong>クローン元の環境と同一のパッチ適用レベル</strong>で構築。</li>
	<li>Engine Yard Cloudダッシュボードから<strong>クリック感覚で構築</strong>可能。</li>
</ul>
例えば、アプリケーション開発プロジェクトが始まったばかりであれば、まずは「開発環境」を構築することから始めるでしょう。その場合には、「開発環境」をベースに、必要になった時に「ステージング環境」や「本番環境」をクローン機能によって構築することが可能になります。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Use_Case_1.png"><img class="alignnone size-large wp-image-1909" alt="Clone_Use_Case_1" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Use_Case_1-1024x313.png" width="1024" height="313" /></a>

また、既に本番稼働しているケースであれば、「本番環境」をベースに必要になった時に改めて「開発環境」を構築し、新たなアプリケーションをデプロイして検証を行い、さらにその「開発環境」をベースに「ステージング環境」を構築するようなニーズもあるでしょう。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Use_Case_2.png"><img class="alignnone size-large wp-image-1910" alt="Clone_Use_Case_2" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Use_Case_2-1024x187.png" width="1024" height="187" /></a>

このように、まったく同一のアプリケーション環境を複数構築するニーズに、Engine Yardはクリック感覚で利用できるクローン機能でお応えします。

&nbsp;
<h3>Engine Yardのクローン機能を使ってみる</h3>
Engine Yard Cloudでは、ダッシュボードと呼ばれるGUIの画面から次の手順で簡単にクローン環境を構築できます。
<ol>
	<li><strong>アプリケーション環境のスナップショットを取得</strong>
Engine Yard Cloudのアプリケーション環境の詳細ページに表示される「<strong>Snapshot</strong>」ボタンをクリックします。<br><br>因みに「スナップショット」とは、アプリケーション環境を再構築する際に必要不可欠なデータ領域のバックアップです。例えば、デプロイ済のアプリケーションや、データが蓄積されたデータベースなどに相当します。<br><br><a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Step1.png"><img class="alignnone size-full wp-image-1943" alt="Clone_Step1" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Step1.png" width="780" height="894" style="border:1px solid black"/></a><br><br></li>
	<li><strong>クローン環境を構築</strong>
Engine Yard Cloudのアプリケーション環境の詳細ページの下部にある「<strong>Clone environment</strong>」リンクをクリックします。<br><br><a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Step2.png"><img class="alignnone size-full wp-image-1942" alt="Clone_Step2" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Step2.png" width="780" height="894" style="border:1px solid black"/></a><br><br>遷移したページで、各種フィールドに値を入力して「<strong>Clone Environment</strong>」ボタンをクリックします。各種フィールドの入力値がデフォルトでよければ「<strong>Clone Environment</strong>」ボタンをクリックするだけです。<br><br><a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Step3.png"><img class="alignnone size-full wp-image-1941" alt="Clone_Step3" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Step3.png" width="780" height="894" style="border:1px solid black"/></a></li>
</ol>
このステップを、2分程度のデモ動画にまとめたものを以下にご紹介します。どうぞご覧ください。

http://youtu.be/BArbN4d6s44

&nbsp;
<h3>Engine Yardのクローン機能の仕組みを知る</h3>
ではここからは、 Amazon Web Services (以降AWSと記載)をインフラ基盤としたEngine Yard Cloudの場合を例にEngine Yardのクローン機能の内部の仕組みをご紹介します。

現行のAWS基盤のEngine Yard Cloudでは、Engine Yardが用意したGentoo LinuxのAMI (マシンイメージ)をベースに、データベース用 EC2インスタンス、アプリケーション用 EC2インスタンス、ユーティリティ用 EC2インスタンス<strong>(*)</strong>がプロビジョニングされます。そして、アプリケーション環境の稼働上、決して消えてはならないデータ領域は永続領域であるAmazon EBS (以降EBSと記載)ボリュームとして各インスタンスにマウントされています。<br><br>
<strong>(*):</strong> <em>ユーティリティ インスタンスとは、お客様のニーズに応じて利用できるインスンタンスです。インスタンス管理サーバー、ログ管理サーバー、MongoDBなど、あらゆる用途にご利用いただけます。</em>
<ol>
<ul>
	<li><strong>データベース インスタンスの永続領域：</strong>/db ディレクトリ</li>
	<li><strong>アプリケーション インスタンスの永続領域：</strong>/data ディレクトリ</li>
	<li><strong>ユーティリティ インスタンスの永続領域：</strong>/data ディレクトリ</li>
</ul>
</ol>
では、改めて、上でご紹介したクローン環境構築の2つのステップ毎に仕組み示します。
<ol>
	<li><strong>アプリケーション環境のスナップショットを取得</strong>
Engine Yard Cloudの「Snapshot」ボタンを押下することで、明示的にデータベースとアプリケーションのそれぞれのマスターインスタンスにマウントされているEBSボリュームが、スナップショットとしてAmazon S3 (以降S3と記載)にストアされます。<br><br>下図のグレーの太矢印がスナップショット取得の流れを示しています。<br><br><a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Source_Environment.png"><img class="alignnone size-full wp-image-1917" alt="Clone_Source_Environment" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Source_Environment.png" width="885" height="770" /></a></li>
	<li><strong>クローン環境を構築
</strong>クローン元のアプリケーション環境のシステム構成とまったく同一のシステム構成のクラスターを、Engine YardのGentoo LinuxのAMIをベースにプロビジョニングし、クローン元と同一のパッチレベルに整え、データベースとアプリケーションのそれぞれの最新のS3スナップショットからEBSボリュームを作成して、EC2インスタンスにマウントします。<br><br>下図のグレーの太矢印がS3からEBSボリュームを作成する流れを示しています。<br><br><a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Target_Environment.png"><img class="alignnone size-full wp-image-1918" alt="Clone_Target_Environment" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Clone_Target_Environment.png" width="885" height="770" /></a></li>
</ol>
Engine Yardは、このような仕組みでクローン環境を構築しています。

この例では簡単のため、ユーティリティ インスタンスを用いないシステム構成で説明をしていますが、ユーティリティ インスタンスについても、クローン機能の対象インスタンスとして動作します。

なお、クローン機能では、New Relicなどのアドオン機能の有効化設定、cronジョブの設定、そしてカスタムChefレシピの設定については引き継がれません。クローン環境にも設定が必要な場合には、それらの設定が必要であることにご注意ください。

&nbsp;
<h3>参考情報</h3>
ここでは、本トピックに関連して参考になる情報のリンクをご紹介します。必要に応じて、ご覧いただければと思います。
<ol>
<ul>
	<li><a title="The Twelve-Factor App - X. Dev/prod parity (英語版)" href="http://12factor.net/dev-prod-parity" target="_blank">The Twelve-Factor App - X. Dev/prod parity (英語版)</a></li>
	<li><a title="The Twelve-Factor App - X. Dev/prod parity (日本語版)" href="http://twelve-factor-ja.herokuapp.com/dev-prod-parity" target="_blank">The Twelve-Factor App - X. Dev/prod parity (日本語版)</a></li>
	<li><a title="Qiita: ウェブ開発で大切な3つの環境: 開発・ステージング・プロダクション" href="http://qiita.com/suin/items/004679b27d4a1f8bcb36" target="_blank">Qiita: ウェブ開発で大切な3つの環境: 開発・ステージング・プロダクション</a></li>
	<li><a title="Engine Yard開発者センター: Clone an Environment (英語版)" href="https://support.cloud.engineyard.com/entries/21009907?locale=67" target="_blank">Engine Yard開発者センター: Clone an Environment (英語版)</a></li>
</ul>
</ol>
&nbsp;
<div><a href="http://ey.io/noyakshave"><img class="alignnone size-full wp-image-1889" style="border: 1px solid black;" alt="noyakshave_seminar_small" src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png" /></a></div>
