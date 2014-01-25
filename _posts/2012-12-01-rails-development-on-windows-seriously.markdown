---
layout: post
status: publish
published: true
title: (マジに) Windows で行う Rails 開発 (翻訳版)
author: evanmachnic
author_login: evanmachnic
author_email: evanmachnic@engineyard.com
wordpress_id: 336
wordpress_url: http://www.engineyard.co.jp/blog/?p=336
date: 2012-12-01 04:39:16.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">
本記事は<a href="http://www.engineyard.com/blog/2012/rails-development-on-windows-seriously/" target="_blank">英語版ブログで2012年2月29日に公開された記事</a>の翻訳版です。
</div>
私は Windows が大好きです。ウェブを見たり、E メールのチェックや Word 文書の作成 (まだ Word を使っていればの話ですが) が本当に簡単で、Windows はうちの祖母でも使えるくらい、どこにでも浸透しているから、大好きです。

それと同時に、私は Windows が大嫌いです。.NET 以外のものを使ってプログラミングをしようものなら、もう苦戦の連続ですから。

この投稿の題名は「(マジに) Windows で行う Rails 開発」です。ここでは Windows の世界で Rails 開発者として仕事をすることの過去、現在、そして未来について語り、成功を収めるために必要なツールをいくつかご紹介したいと思います。
<h2>過去</h2>
格好悪いのであまり言いたくないのですが、実は私は Ruby on Rails のプログラミングを Windows 環境で始めた一人です。それは 2008 年秋のことで、Windows Vista を使っていました。

もう怖くて震えが止まらないでしょう?

不良なリリースの質はさて置き、とりあえず最大限に活用しました。プログラミングは授業で習ったことしかなかったので、Aptana RadRails をインストールしたところ、そのまま直降下して墜落しました。

あの頃は基本的に言って Windows に Rails をインストールする方法は 2 つありました。
<ol>
	<li><a href="http://jruby.org/">JRuby</a> をインストールして Java 仮想マシン上で実行する</li>
	<li><a href="http://rubyinstaller.org/">RubyInstaller</a> 実行可能ファイルと <a href="http://rubyinstaller.org/add-ons/devkit/">DevKit</a> をダウンロードして、すべて手動でインストールする</li>
</ol>
JRuby がどんなものか、なぜ必要なのかもわからず、自分が何をしているかも定かでなかった私は、後者のオプションを選びました。RadRails でインストールする方法もあったかも知れませんが、果たして機能するものか大きな疑問でした。

既定の設定をすべて受け入れさえすれば、すべてが正常にインストールされ、言うことなしでした。しかし、別のパスに Ruby をインストールしようものなら、これは神様に助けてもらうしかありません。

Ruby をこの方法でインストールするにあたって最大の問題は、DevKit を取得しないと C の機能拡張を一切構築できなかったことです。ところで Ruby は C で書かれているので、構築に C の機能拡張が必要となるライブラリがごまんとあります。ただ単にウェブ アプリケーションを書きたかった初心者がこのようなエラーに行き当たるとは、実に最悪でした。
<h2>現在</h2>
では 2012 年に早送りして、Windows を使用する Rails 開発者にとって最大の救世主 <a href="http://railsinstaller.org/">RailsInstaller</a> の登場です。これは Wayne E. Seguin 氏が開発・管理しています。

同氏は <a href="http://rvm.beginrescueend.com/">Ruby Version Manager</a>、<a href="http://bdsm.beginrescueend.com/">SM Framework</a>、そして <a href="http://railsinstaller.org/">RailsInstaller</a> の開発努力に余念がありません。しかも、すべてコミュニティのために大奉仕されているので、もし道で見かけるようなことがあったらぜひ一杯奢ってあげてください。

RailsInstaller は、Ruby on Rails のプログラミングを始めるために必要なものをすべてパッケージにしてくれる、実に素晴らしいソフトウェアです。このソフトには既定で <a href="http://ruby-lang.org/">Ruby</a>、<a href="http://rubyonrails.org/">Rails</a>、<a href="http://gem-bundler.com/">Bundler</a>、<a href="http://git-scm.com/">Git</a>、<a href="http://www.sqlite.org/">Sqlite</a>、<a href="https://github.com/rails-sqlserver/tiny_tds">TinyTDS</a>、そして厄介な C 拡張メソッド用の <a href="http://rubyinstaller.org/add-ons/devkit/">DevKit</a> が含まれており、おまけに <a href="https://github.com/rails-sqlserver">SQLServer</a> のサポートも受けることができます。これらのコンポーネントをすべて探し出し、別々にインストールするのは悪夢のような作業です。
<h2>未来</h2>
正直なところ未来は予言できませんが、事態は過去よりも改善されていくことは確かでしょう。これまで長い道を歩んできましたが、まだまだ大事な仕事は残っています。

RailsInstaller をインストールして Ruby on Rails 環境が整ったところで、次はどうしたらよいのでしょう。
<h2>必要なもの</h2>
次に、Windows の Rails 開発者として成功するためにどうしても必要なものをいくつか挙げます。
<h3>Git</h3>
<a href="http://en.wikipedia.org/wiki/Revision_control">ソース コード管理</a>で変更を追跡していない方は、すぐに始めてください。誰が何と言おうと、とにかく <a href="http://git-scm.com/">Git</a> が一番です。Git の最高の特徴は Git が<em>ディストリビュート</em>されるという点です。したがって、完全なコード リポジトリが<em>誰でも</em>手に入るので、Subversion サーバーで待機する必要がないのです。<a href="http://github.com/">Github</a> というのもあります。もし使ったことがない方は、こちらも素晴らしいですよ。Github は、コーディングにソーシャル機能を加え、コラボレーションを行いやすくします。

とは言え、どのソース コード管理ツールを使おうが、正直なところ何かしら使っていれば問題ありません。index.html.old を作成するのはやめましょう。この方法は信頼性に欠ける上、コード ホスティング サービスを利用していればコンピューターのクラッシュを心配する必要はありません。それに Windows を実行しているので、これはいずれにせよ毎日何度か心配になることです。
<h3>Pik</h3>
<a href="http://rvm.beginrescueend.com/">Ruby Version Manager</a>、略して RVM も、Seguin 氏が開発した素晴らしいツールの 1 つです。Ruby の異なるバージョンを簡単に管理でき、さまざまなプロジェクトにサンドボックス環境を提供してソフトウェアの互換性をテストできるようにします。しかし、残念ながら Windows では動作しません。

次善のツールとして <a href="http://github.com/vertiginous/pik">Pik</a> があります。Pik を使用して、JRuby や IronRuby を含めさまざまなバージョンの Ruby をインストールできます。RVM に備わっている付属機能はありませんが、このツールなしで複数の Ruby を実行しようとすると大変なことになります。Pik は <a href="https://gist.github.com/github.com/vertiginous/pik">Github ページ</a>から入手できます。
<h3>IDE 対テキスト エディター</h3>
次は実際にアプリケーションを記述するためのツールが必要です。ここでは Visual Studio は使いません。Rails との相性が悪いようです。エディターには <a href="http://en.wikipedia.org/wiki/Text_editor">テキスト エディター</a>か<a href="http://en.wikipedia.org/wiki/Integrated_development_environment">統合開発環境 (IDE: Integrated Development Environment)</a> のどちらかを選択します。以下に挙げるオプションはすべてマルチプラットフォーム対応なので、Windows、Mac、Linux のいずれでも使用できます。
<h4>IDE</h4>
一体型のパッケージに慣れている方には、<a href="http://www.jetbrains.com/ruby/">JetBrains RubyMine</a> と <a href="http://aptana.org/products/studio3">Aptana Studio</a> がお勧めです。RubyMine は有料ですが、最も洗練度が高く、アプリケーションの編集、テスト、そしてデプロイを行う機能がこれでもかというほど用意されています。

Aptana Studio は無料で、RubyMine にコストをかけたくない場合には、代わりに利用できる優れものです。Eclipse をベースに構築されているので、Java 開発者の方には使いやすいでしょう。
<h4>テキスト エディター</h4>
私が好きなのはテキスト エディターを使う方法です。大部分の Rails 開発者もこの方法を選びます。お勧めのエディターはいくつかありますが、メモ帳だけは推奨できません。

<a href="http://www.vim.org/">Vim</a> は歴史が古く実績のあるツールです。拡張性が抜群で、非常に高速です。Vim は習得が大変だという人が多いようですが、手始めに知っておく必要があるのはほんの一握りのコマンドで、あとは作業をしながら覚えることができます。Vim の最高のメリットは、コマンドラインから起動して編集を始められる点です。

<a href="http://www.sublimetext.com/">SublimeText</a> もなかなか人気があります。料金が多少かかりますが、Ruby と Rails のサポートが組み込まれています。是非試してみることをお勧めします。

<a href="http://redcareditor.com/">Redcar</a> は素晴らしいエディターで、実は Ruby で書かれています。そのため、拡張機能を記述するのに別の構文を学ぶ必要がないので、簡単に拡張できます。また、Redcar では TextMate バンドルがサポートされるため、どんな必要に対しても拡張機能が見つかると思います。
<h2>何かを学ぶ</h2>
Rails は素晴らしいコミュニティによってサポートされています。おかげで従来よりずっと簡単に Ruby on Rails アプリケーションの正しい書き方を学ぶことができ、あらゆる学習スタイルに合ったリソースが手に入ります。
<h3>スクリーンキャスト</h3>
<a href="http://railscasts.com/">Railscasts</a> はすごい量の知識で溢れているので、紹介しないわけにはいきません。ここでは Ryan Bates 氏が 2007 年 (?) 以来 Rails に関するトピックのスクリーンキャストを毎週アップし続けています。長さは大体 10 ～ 15 分で毎回 1 つのトピックが扱われます。アプリケーションに素早く簡単に認証を追加する方法を学びたい場合などは Railscasts を是非覗いてみましょう。
<h3>チュートリアル</h3>
なんといっても最高のチュートリアルは Michael Hartl 氏の『<a href="http://ruby.railstutorial.org/">RailsTutorial</a>』です。Ruby、Rails、およびテスト重視の開発について詳細が説明されています。この本の HTML バージョンは無料で、PDF バージョンを購入することもできます。それでも足りないという方には、スクリーンキャストも提供されています。

そのほかにも <a href="http://rubyonrails.org/">rubyonrails.org</a> や <a href="http://www.google.com/search?q=ruby+on+rails">Google 検索</a>で多くのチュートリアル、スクリーンキャスト、ドキュメントを見つけることができます。
<h2>成果を共有する</h2>
では、初めて作成した Ruby on Rails アプリケーションをどうしたらよいでしょう。せっかくクールなアプリケーションが出来たんですから、世界中のユーザーと共有しましょう。厄介な仕事はやめ、Windows サーバーにデプロイしようなどという考えはさっさと忘れてください。幸い今日ではクラウド プラットフォームのプロバイダーがいくつもあるので、自分でサーバーをセットアップする必要もありません。私のお気に入りはもちろん Engine Yard ですが、ほかのオプションもあります。自分に合ったものを探してみましょう。
<h2>注意書き</h2>
Windows での Rails アプリケーション開発には、主に複数のプラットフォームをサポートする場合に気を付けたい重要な注意事項が 1 つあります。多くの Windows システムでは gem を正しく機能させるためにバイナリを何度も要求するため、gem の開発者は Unix と Windows 用に別のバージョンをリリースします。Unix 環境にデプロイしている場合、デプロイする場所に Unix バージョンをインストールする必要があります。
<h2>トラブルシューティング</h2>
何かしらの問題が発生するのは避けられません。数多くのマニュアルや文書が利用できますが、それでも支援を受ける方法を知っておくと役に立ちます。
<h3>Ruby on Rails Guides</h3>
「<a href="http://guides.rubyonrails.org/">Ruby on Rails Guides</a>」は、その名のとおり Rails の公式ドキュメントです。大抵、Rails の一般的トピックを調べたい場合は最初にチェックすると役立ちます。
<h3>フォーラム</h3>
ガイドでは扱われていないトピックの場合、質の高いフォーラムを利用するのが便利です。<a href="http://stackoverflow.com/">StackOverflow</a> は、プログラミングのヘルプではおそらく一番広く利用されているフォーラムです。質問や回答ができるほか、活動に応じてポイントも取得できます。質問は Google でインデックス化されているので、Google 検索をうまく構成すると、役に立つ結果が返されます。
<h3>IRC</h3>
他の方法では解決できないときに私が利用しているのは IRC です。IRC は <a href="http://en.wikipedia.org/wiki/Internet_Relay_Chat">Internet Relay Chat (インターネット リレー チャット)</a> の略称です。個人的にはファンではありませんが、IRC は長年利用されていて、問題について他のユーザーとリアルタイムでチャットすることができます。

IRC ルームを頻繁に訪れる場合、優れたデスクトップ クライアントが必要です。私は <a href="http://www.mirc.com/">mIRC</a> を問題なく利用した経験がありますが、ほかにも数多くのクライアントが出回っています。どのクライアントを選ぶにしても、#Rails と #RailsInstaller の各ルームだけは必ずチェックしましょう。
<h2>次のステップ</h2>
この記事は情報が多すぎると思われるかも知れません。しかし、実際はまだまだ奥が深く、皆さんの精神衛生のためなるべく簡潔にしたつもりです。私の講演に使用したスライドに興味がある方は、<a href="http://emachnic.github.com/rails_dev_windows">emachnic.github.com/rails_dev_windows</a> を参照してください。

一番効果があるのは、とにかくソフトウェアを入手して何か作ってみることです。いくら参考書を熟読しスクリーンキャストを眺めても、実際にアプリケーションを作成しなければ知識が自分のものになりません。ヘルプが必要になったら上記のリソースを利用したり、<a href="http://broadmac.net/interact">emachnic</a> を目安に私にオンラインでコンタクトすることも可能です。それでは、グッドラック、そして楽しいプログラミングを!

&nbsp;

Wayne E. Seguin 氏、<a href="https://twitter.com/#!/luislavena" target="_blank">Luis Lavena</a> 氏、<a href="http://metaskills.net" target="_blank">Ken Collins</a> 氏をはじめとする RailsInstaller および RubyInstaller チームの皆さん、そして Windows での Rails 開発の苦痛を少しでも和らげるために貢献してくださった方々全員に心から感謝いたします。皆さんの助力がなければ、この道のりはもっとずっと険しいものになっていたはずです。世界中の開発者すべてを代表して、感謝の辞を捧げたいと思います。
