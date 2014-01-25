---
layout: post
status: publish
published: true
title: 'Homebrew: OS X に欠けていたパッケージ マネージャー (翻訳版)'
author: andrearko
author_login: andrearko
author_email: andrearko@engineyard.com
wordpress_id: 343
wordpress_url: http://www.engineyard.co.jp/blog/?p=343
date: 2012-12-19 08:17:59.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">
本記事は<a href="http://www.engineyard.com/blog/2010/homebrew-os-xs-missing-package-manager/" target="_blank">英語版ブログで2010年2月2日に公開された記事</a>の翻訳版です。
</div>
Unix におけるソフトウェア パッケージの管理作業はごく控えめに表現しても「非常に厄介な代物」であり、大部分の Linux ディストリビューションはこの厄介を緩和しようというさまざまな試みに合わせて構築されています。この投稿では、<a href="http://github.com/mxcl/homebrew">Homebrew</a> という、パッケージ管理を簡易化する素晴らしい新オプションをご紹介したいと思います。

Homebrew がリリースされるまで、OS X 用の効果的なパッケージ マネージャーを作成するためにさまざまな試みがなされてきました。中でも <a href="http://finkproject.org">Fink</a> と <a href="http://macports.org">MacPorts</a> の 2 つは人気の高いオプションでしたが、どちらにも不都合な点がありました。どちらを使用しても、パッケージや Portfile の作成は依然として<em></em>複雑で困難だったのです。

<a href="http://www.methylblue.com/">Max Howell</a> 氏が開発した Homebrew は、編集が容易で新しいパッケージを簡単に作成できる、素晴らしいツールです。では、さっそく中身をご紹介することにしましょう。
<h2>機能の概要</h2>
唄い文句はいたって簡単です。Homebrew は、OS X で行う Unix ソフトウェア パッケージのダウンロードとインストールの単調な繰り返し作業を軽減してくれます。<code>./configure &amp;&amp; make &amp;&amp; make install</code> はもうたくさん、という方には Homebrew が役立ちます。
<h2>Homebrew のメリット</h2>
前述のように、OS X には既に <a href="http://finkproject.org">Fink</a> と <a href="http://macports.org">MacPorts</a> という 2 つのパッケージ マネージャーが備わっています。このどちらかで十分間に合っているという方は問題ありません。しかし、過去の経験からこれらのツールに不満を感じた方は、是非 Homebrew を試してみましょう。Homebrew のコアは数百行の Ruby コードだけで作成されており、 formula の作成や編集だけでなく、Homebrew <em>自体</em>の編集も簡単に行えます。

外部構造が強制されることもありません。既定の設定では <code>/usr/local</code> にインストールされますが、任意の場所にインストールできます。Homebrew ディレクトリ内では、Homebrew の <em>cellar</em> にあるサブディレクトリ (<code>Cellar/git/1.6.5.4/</code> など) にソフトウェアがインストールされます。インストール後、Homebrew はソフトウェアから標準の Unix ディレクトリへのシンボリック リンクを作成します。まだ正式には Homebrew の一部となっていないパッケージやバージョンを手作業でインストールしたい場合には、同じ場所に問題なく共存させることが可能です。

ただ、バージョン コントロールから直接に formula をインストールできるので、通常このような作業は必要ありません。パッケージにパブリックの git、svn、cvs、または一定しないリポジトリが含まれる場合、単に <code>brew install</code> と入力するだけで最新の開発バージョンを何度でもインストールできます。

Homebrew はパッケージの重複をできる限り回避するので、パッケージのインストールも速くなります。OS X に既に Perl の<em>機能的</em>インストールが組み込まれているので、パッケージの依存関係のために<em>さらに別</em>バージョンの Perl をインストールする必要はありません。そして何よりも、Homebrew には、コンピューターでソフトウェアのインストールや管理を行うために sudo を使う必要はないという基本理念があります。
<h2>入手方法</h2>
Homebrew が依存する唯一の要素である <a href="http://developer.apple.com/tools/">OS X Developer Tools</a> は、OS X のインストーラー ディスクに搭載されているほか、Apple から無償でダウンロードできます。

特別な理由がない限り、Homebrew は <code>/usr/local</code> にインストールするのが一番簡単です。インストール作業はコマンドラインでいくつかの手順を実行するだけです。
<pre escaped="true"># Take ownership of /usr/local so you don't have to sudo
sudo chown -R `whoami` /usr/local
# Fix the permissions on your mysql installation, if you have one
sudo chown -R mysql:mysql /usr/local/mysql*
# Download and install Homebrew from github
curl -L http://github.com/mxcl/homebrew/tarball/master | tar xz --strip 1 -C /usr/local</pre>
これが済んだら準備は完了です。PATH に <code>/usr/local/bin</code> があると仮定して、次を試してみましょう。
<pre escaped="true">brew install wget
brew info git</pre>
Homebrew wiki には、<a href="http://github.com/mxcl/homebrew/wiki/Gems,-Eggs-and-Perl-Modules">RubyGems、CPAN、および Python の EasyInstall との統合</a>についての詳細情報も記載されています。

Homebrew のコピーを最新状態に保つのも簡単です。
<pre escaped="true">brew install git
brew update</pre>
git をインストールしたら、<code>brew update</code> をいつでも実行して最新の formula を取得できます。
<h2>コントリビューション</h2>
新しい formula の作成も、同じくらい簡単です。Homebrew に wget 用の formula がない場合は、次のような formula を作成できます。
<pre escaped="true">brew create http://ftp.gnu.org/gnu/wget/wget-1.12.tar.bz2</pre>
 formula を保存した後、<code>brew install -vd wget</code> を使用してテストを行い、詳細ログとデバッグ モードを有効にできます。 formula を正しく機能させるためにヘルプが必要な場合は、<a href="http://wiki.github.com/mxcl/homebrew/contributing">Homebrew wiki</a> に詳細なドキュメントがあります。また、<a href="http://github.com/mxcl/homebrew/tree/master/Library/Formula/git.rb">git</a> や <a href="http://github.com/mxcl/homebrew/tree/master/Library/Formula/flac.rb">flac</a> などの既存の formula を手本にして学ぶこともできます。

Homebrew の多数のサンプル formula や内部の仕組みを確認するには、<code>brew edit</code> を実行します。コードはわかりやすく書かれています。Homebrew について質問がある場合や今後の計画について知りたい場合は、Homebrew のコントリビューターが集まる Freenode の #machomebrew チャンネルをチェックしてみましょう。

正しく機能する formula が出来上がったら、GitHub で自分の Homebrew フォークを作成して新しい formula をプッシュするのは簡単です。これには github gem を使用します。
<pre escaped="true">git add .
git commit -m "Added a formula for wget"
gem install json github
github fork
git push &lt;your github username&gt; mastergitx</pre>
GitHub に変更をプッシュしたら、<a href="http://github.com/mxcl/homebrew/issues">Homebrew 問題追跡ページ</a>にアクセスして「New formula:」という件名のチケットを作成してください。特に問題がなければ formula はメインの Homebrew リポジトリに追加され、誰でもこれを使用できるようになります。
<h2>最後に</h2>
Homebrew は MacPorts や Fink に代わる魅力的なツールです。Homebrew のコアおよびすべての formula が Ruby で書かれているので、新しいパッケージや新機能を簡単に追加できます。Mac にインストールした Unix ソフトウェアをよりうまく制御したい方や、他のパッケージ マネージャーに不満を感じてきた方は、Homebrew を是非お試しください。きっと嬉しい驚きを感ずることと思います。
