---
layout: post
status: publish
published: true
title: 安定版 RVM と関連情報 (翻訳版)
author: michalpapis
author_login: michalpapis
author_email: michalpapis@engineyard.com
excerpt: "<div class=\"note\">\r\n本記事は<a href=\"http://www.engineyard.com/blog/2012/rvm-stable-and-more/\"
  target=\"_blank\">英語版ブログで2012年1月24日に公開された記事</a>の翻訳版です。\r\n</div>\r\n\r\n安定版 RVM
  がリリースされてしばらくになります。RVM で行われる処理について把握している方は多いと思いますが、それ以外にも大事な情報があります。\r\n\r\n現在の RVM
  は、<a href=\"http://nvie.com/posts/a-successful-git-branching-model/\">ここ</a>で説明されているモデルに従い
  <code>git flow</code> を使用していますが、これは RVM のリリース モデルに大きな変更を加えるものです。<code>master</code>
  ブランチを使ったマイナー リリースは今後行いません。これからは、メジャーな (latest という) リリースのみを時々公開します。ただし、Ruby バージョンの更新などの重要なアップデートと修正プログラムのみを取り入れる安定
  (stable) ブランチは維持管理していきます。この新しいリリース モデルによって、本番環境用に安定バージョンの RVM を維持しながら、<code>head</code>
  で新機能を開発することが可能になります。\r\n\r\n安定版 RVM をインストールするには:\r\n<pre escaped=\"true\">$ bash
  -s stable &lt; &lt;(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)</pre>\r\n安定版
  RVM を更新するには:\r\n<pre escaped=\"true\">$ rvm get stable # the same as:\r\n$ rvm get
  branch wayneeseguin/stable</pre>\r\nまた、RVM 用に独自の修正プログラムを使用することもできます。これはコントリビューターには特に便利です。コントリビューターはプル要求を送信する前に、自分の作業内容をテストしたり、他のユーザーにテストを依頼したりできます。プロジェクトを分岐して、変更を追加し、コミットしてからプッシュするだけで、誰でもその分岐にインストールや更新を行えるようになります。\r\n<pre
  escaped=\"true\">$ rvm get branch mpapis/master</pre>\r\nRVM はインストールの経過時間に関する情報を提供します。インストール後の経過時間を正確に知るには、次を実行します。\r\n<pre
  escaped=\"true\">$ rvm info rvm\r\nrvm:\r\nversion:      \"rvm 1.10.0 by Wayne E.
  Seguin &lt;wayneeseguin@gmail.com&gt;, Michal Papis &lt;mpapis@gmail.com&gt; [https://rvm.beginrescueend.com/]\"\r\nupdated:
       \"2 hours 52 minutes 49 seconds ago\"</pre>\r\n"
wordpress_id: 350
wordpress_url: http://www.engineyard.co.jp/blog/?p=350
date: 2013-01-01 08:35:39.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">
本記事は<a href="http://www.engineyard.com/blog/2012/rvm-stable-and-more/" target="_blank">英語版ブログで2012年1月24日に公開された記事</a>の翻訳版です。
</div>

安定版 RVM がリリースされてしばらくになります。RVM で行われる処理について把握している方は多いと思いますが、それ以外にも大事な情報があります。

現在の RVM は、<a href="http://nvie.com/posts/a-successful-git-branching-model/">ここ</a>で説明されているモデルに従い <code>git flow</code> を使用していますが、これは RVM のリリース モデルに大きな変更を加えるものです。<code>master</code> ブランチを使ったマイナー リリースは今後行いません。これからは、メジャーな (latest という) リリースのみを時々公開します。ただし、Ruby バージョンの更新などの重要なアップデートと修正プログラムのみを取り入れる安定 (stable) ブランチは維持管理していきます。この新しいリリース モデルによって、本番環境用に安定バージョンの RVM を維持しながら、<code>head</code> で新機能を開発することが可能になります。

安定版 RVM をインストールするには:
<pre escaped="true">$ bash -s stable &lt; &lt;(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)</pre>
安定版 RVM を更新するには:
<pre escaped="true">$ rvm get stable # the same as:
$ rvm get branch wayneeseguin/stable</pre>
また、RVM 用に独自の修正プログラムを使用することもできます。これはコントリビューターには特に便利です。コントリビューターはプル要求を送信する前に、自分の作業内容をテストしたり、他のユーザーにテストを依頼したりできます。プロジェクトを分岐して、変更を追加し、コミットしてからプッシュするだけで、誰でもその分岐にインストールや更新を行えるようになります。
<pre escaped="true">$ rvm get branch mpapis/master</pre>
RVM はインストールの経過時間に関する情報を提供します。インストール後の経過時間を正確に知るには、次を実行します。
<pre escaped="true">$ rvm info rvm
rvm:
version:      "rvm 1.10.0 by Wayne E. Seguin &lt;wayneeseguin@gmail.com&gt;, Michal Papis &lt;mpapis@gmail.com&gt; [https://rvm.beginrescueend.com/]"
updated:      "2 hours 52 minutes 49 seconds ago"</pre>
<a id="more"></a><a id="more-350"></a>RVM の出力形式が、特にインストールと <code>get</code> / <code>notes</code> アクションに関して大きく変わったので注意が必要です。RVM のインストールと更新に際して表示される情報の量が減り、その内容はわかりやすくなっています。<code>rvm notes</code> コマンドを実行すると、以前インストールや更新プロセスで表示されていた重要なメモがすべて表示されます。RVM を更新すると、メモの最新の更新だけが表示されます。インストールの後で毎回 <code>rvm notes</code> を実行する必要はありません。
<pre escaped="true">$ rvm get head
...
Upgrade Notes:
* If you see the following error message: Unknown alias name: 'default'
re-set your default ruby, this is due to a change in how default works.
...</pre>
この後すぐにもう一度実行すると、新しいメモはないことがわかります。
<pre escaped="true">$ rvm get head
...
Upgrade Notes:
* No new notes to display.
...</pre>
最近加えられたもう 1 つの便利な変更は、<code>rvm get ...</code> の後で自動的に <code>rvm reload</code> を実行する機能です。
<pre escaped="true">$ rvm get head
...
RVM reloaded!</pre>
</div>
<h3>重要な変更点</h3>
<div>

バイナリから ruby を <code>use</code> する方法は、初心者から経験者まで多くのユーザーの混乱を招きました。RVM がシェル関数として読み込まれており、関数ではなくバイナリ スクリプトを呼び出す場合、その ruby はアクティブになりません。これは、外部コマンドまたは "バイナリ" は、その呼び出された環境に影響を与えることができないためです。現時点では rvm が (関数ではなく) バイナリとして呼び出されると、次の警告が表示されます。
<pre escaped="true">$ command rvm use 1.9.3
RVM is not a function, selecting rubies with 'rvm use ...' will not work.
$ rvm use 1.9.3
Using /home/mpapis/.rvm/gems/ruby-1.9.3-p0</pre>
以前はスクリプトで <code>--default</code> スイッチを使ってバイナリを呼び出し、特定の ruby を既定にする便利な方法がありました。これを行う新たな方法は、既定のエイリアスを明示的に作成することです (これは <code>--default</code> フラグに対しバックグラウンドで実行されていました)。
<pre escaped="true">$ rvm alias create default &lt;version&gt;</pre>
RVM は、ruby が存在する場合に新しい ruby をインストールすることはなくなりました。
<pre escaped="true">$ rvm install 1.9.3</pre>
クリーンな再インストールを行うには、<code>reinstall</code> アクションを使用する必要があります。
<pre escaped="true">$ rvm reinstall 1.9.3</pre>
事前にソースのクリーンアップを行わずに、上から被せてインストールする従来の方法は、<code>--force</code> フラグを使って引き続き利用できます。
<pre escaped="true">$ rvm install 1.9.3 --force</pre>
RVM では多くの修正プログラムが公開されてきたので、一部の変更にはシステム ファイルの更新が必要となります。これらのファイルを更新するには、<code>--auto</code> スイッチを使用します。これは特にマルチユーザー インストールには非常に便利です。この方法は RVM からの最新設定を提供するために /etc のファイルを更新するので、root または system インストールとも呼ばれます。
<pre escaped="true">$ rvm get head --auto</pre>
もう 1 つの重要な変更は、RVM に 3 番目のインストール タイプである mixed モードが追加されたことです。このモードでは、すべてのユーザーが自分のプライベートな ruby や gemset の使用を指定できます。
<pre escaped="true">$ rvm user [gemsets/all]</pre>
また Linux では、sysadmin が、<code>--skel</code> フラグ (これは /etc/skel を更新します) で作成されるすべての新規ユーザー用に既定で RVM の設定を定義できるようにもなりました。
<pre escaped="true">$ sudo rvm user [gemsets/all] --skel</pre>
</div>
<div>従来から RVM の目標は、さまざまな ruby バージョンの管理を容易にすることでした。この目標をさらに実現に近づけるため、新しいインストール スイッチがいくつか実装されています。JRuby / Rubinius で既定モードを設定するには、<code>--18</code> フラグと <code>--19</code> フラグが使用できます。
<pre escaped="true">$ rvm install rbx --19   # will install Rubunius with default mode set to 1.9
$ rvm install jruby --18 # will install JRuby with default mode set to 1.8</pre>
OS X で 32 ビット モードの ruby をコンパイルするには、<code>--32</code>、<code>--64</code>、<code>--universal</code> の各フラグが使用できます。
<pre escaped="true">$ rvm install 1.9.3 --universal # to build fat binary including both 32 and 64 bit binaries
$ rvm install 1.8.7 --32 # to build only 32 bit ruby
$ rvm install 1.8.7 --with-arch=i386 # is equivalent to the 32 bit one, but is available only via RVM, ruby 1.8.7 sources do not support it.</pre>
名前付き ruby には、命名の問題の回避に役立つ追加の検証をがあり、有効な名前だけにインストールが許可されます。
<pre escaped="true">$ rvm install 1.8.7 --32 -n 32 # will fail
$ rvm install 1.8.7 --32 -n n32 # will work
$ rvm install 1.8.7-n32 --32 # equivalent of the above</pre>
最後になりましたが、RVM の表示色管理が改善されています。既定により RVM のコンソールには色付きの出力が表示され、端末が接続されていない場合は色が無効になります。環境変数やコマンドラインのスイッチを使って色を無効にすることもできます。
<pre escaped="true">$ rvm list         # will show the colored list by default in terminal
$ rvm --color=force list | less -R         # will show the colored list in less
$ rvm_pretty_print_flag=auto rvm list | tee my-rubies.list         # will automatically disable colors
$ rvm --color=no list         # will always disable colors</pre>
ここで、もう 1 つ大事なお知らせがあります。今なら OS X ユーザーは新しい便利なツールが手に入ります。公式の RVM GUI <a href="http://unfiniti.com/software/mac/jewelrybox">JewelryBox</a> バージョン 1.2 がリリースされました。このバージョンでは、上で説明した RVM の変更点すべてがサポートされています。
