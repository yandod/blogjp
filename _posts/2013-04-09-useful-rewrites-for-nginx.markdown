---
layout: post
status: publish
published: true
title: Nginx の便利なrewrite (翻訳版)
author: Kevin Rutten
author_login: kevinrutten
author_email: kevinrutten@engineyard.com
excerpt: "<div class=\"note\">\r\n本記事は<a href=\"http://www.engineyard.com/blog/2011/useful-rewrites-for-nginx/\"
  target=\"_blank\">英語版のブログで2011年3月29日に公開された記事</a>の翻訳版です。\r\n</div>\r\n\r\n<span style=\"font-weight:
  normal;\"><img class=\"alignright\" src=\"http://static.howstuffworks.com/gif/diesel-locomotive-engine-2.jpg\"
  alt=\"\" width=\"400\" height=\"300\" />私は Rails での作業に満足していますが、仕事に合った正しいツールを使うことも大事だと考えています。多くの開発者が
  Rails アプリケーションにリダイレクトを追加しますが、開発段階では便利でも、いざ本番環境でのトラフィックが開始されると上手くいかない場合があります。当社では、フロントエンドのリバース
  プロキシとして <a title=\"Nginx\" href=\"http://wiki.nginx.org/Main\" target=\"_blank\">Nginx</a>
  ウェブ サーバーを使用しています。一般的なリダイレクトを Nginx に移して Rails の負担を軽減し、本来のタスクを行わせることが簡単にできます。</span>\r\n\r\nたとえば、最初にフォーカス
  グループでは名前が覚えにくいと言われ、SEO の教祖様にはドメインに www を含めなければならないと批判され、ユーザービリティ担当者からは一般的な入力ミスを検知すべきだと言われたとしましょう。最初のうちは、これらの変更をすべて
  Rails で行うことができます。www がないことを検知した場合は 302 を返します。登録したドメインの入力ミスを検知して、同じく 302 で修正します。しかし、サイトの人気が高まりトラフィックが増大してキューで待機するようになると、リダイレクトもキューに追加されて負荷がますます大きくなります。それならばいっそ、こうしたタスクをウェブ
  サーバーにオフロードしてはどうでしょう。\r\n\r\nこうした操作はすべて Rails アプリケーションで行えますが、フロントエンドで処理するのも同じくらい簡単です。ここでは
  Nginx で特に変わったことをするのではなく、ごく一般的で便利なrewriteについて説明したいと思います。\r\n\r\n<address>メモ<span
  style=\"font-style: normal;\">:AppCloud でクラスターを使用している場合、前の例では \"listen 81;\" を使用する必要があります。Nginx
  の設定で既に指定されている内容を確認してください。</span></address><address><span style=\"font-style: normal;\">"
wordpress_id: 650
wordpress_url: http://www.engineyard.co.jp/blog/?p=650
date: 2013-04-09 14:13:03.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">
本記事は<a href="http://www.engineyard.com/blog/2011/useful-rewrites-for-nginx/" target="_blank">英語版のブログで2011年3月29日に公開された記事</a>の翻訳版です。
</div>

<span style="font-weight: normal;"><img class="alignright" src="http://static.howstuffworks.com/gif/diesel-locomotive-engine-2.jpg" alt="" width="400" height="300" />私は Rails での作業に満足していますが、仕事に合った正しいツールを使うことも大事だと考えています。多くの開発者が Rails アプリケーションにリダイレクトを追加しますが、開発段階では便利でも、いざ本番環境でのトラフィックが開始されると上手くいかない場合があります。当社では、フロントエンドのリバース プロキシとして <a title="Nginx" href="http://wiki.nginx.org/Main" target="_blank">Nginx</a> ウェブ サーバーを使用しています。一般的なリダイレクトを Nginx に移して Rails の負担を軽減し、本来のタスクを行わせることが簡単にできます。</span>

たとえば、最初にフォーカス グループでは名前が覚えにくいと言われ、SEO の教祖様にはドメインに www を含めなければならないと批判され、ユーザービリティ担当者からは一般的な入力ミスを検知すべきだと言われたとしましょう。最初のうちは、これらの変更をすべて Rails で行うことができます。www がないことを検知した場合は 302 を返します。登録したドメインの入力ミスを検知して、同じく 302 で修正します。しかし、サイトの人気が高まりトラフィックが増大してキューで待機するようになると、リダイレクトもキューに追加されて負荷がますます大きくなります。それならばいっそ、こうしたタスクをウェブ サーバーにオフロードしてはどうでしょう。

こうした操作はすべて Rails アプリケーションで行えますが、フロントエンドで処理するのも同じくらい簡単です。ここでは Nginx で特に変わったことをするのではなく、ごく一般的で便利なrewriteについて説明したいと思います。

<address>メモ<span style="font-style: normal;">:AppCloud でクラスターを使用している場合、前の例では "listen 81;" を使用する必要があります。Nginx の設定で既に指定されている内容を確認してください。</span></address><address><span style="font-style: normal;"><a id="more"></a><a id="more-650"></a></span></address>
<h3>古いドメインを新しいドメインに書き換える</h3>
ドメイン名を beta_domain.com から bedom.com に変えることに決定したとします。やはり bedom の方が短く、クールな感じがしますね。この処理は Rails に渡す必要はまったくありません。次のように Nginx で簡単に処理できます。
<pre escaped="true">  server {
    listen 80;
    server_name beta_domain.com www.beta_domain.com;
    rewrite ^ $scheme://www.bedom.com$request_uri permanent;
    # or
    # rewrite ^ $scheme://www.bedom.com ;
  }</pre>
これはシンプルなブロックですが、多くのことを行います。古いドメインと一致するすべての要求を検知して、リダイレクトします。$request_uri のある最初のリダイレクト行は、「リダイレクトの際に URL 部分をコピーする」ことを意味します。したがって、ユーザーが http://www.beta_domain.com/about にアクセスすると、http://www.bedom.com/about にリダイレクトされます。permanent というのは、ブラウザーがこのリダイレクトを永続的に記憶する (ステータス 301) という意味で、これには後で説明するようにリスクが伴います。コメントアウトされている 2 番目のバージョンは、「すべてをホーム ページにリダイレクトする」よう指定する、よりシンプルなコードです。これは、サイトの名前だけでなく、サイト全体を改変した場合に適しています。この 2 番目のバージョンは一時リダイレクト (ステータス302) を返すので、ブラウザーはこの URL を将来再確認します。このブロックに、登録したドメインの一般的な "入力ミス" を追加することができます。
<h3>ドメインに www の追加または削除をを行う</h3>
さて次に、SEO 担当者から、ドメインに www を追加してすべての要求にこれを含めるようお達しがありました。一方で今日になって、Twitter のおかげで、「名前は短い方がクールだ」という理由からこの www を削除するよう指示が出るかも知れません。困りますね。でも、そんな問題も次のコードで簡単に解決されます。
<pre escaped="true">  # Add a www with this block
  server {
    listen 80;
    server_name bedom.com;
    rewrite ^(.*)$ $scheme://www.bedom.com$1;
  }</pre>
<pre escaped="true">  # Remove a www with this block instead
  server {
    listen 80;
    server_name www.bedom.com;
    rewrite ^(.*)$ $scheme://bedom.com$1;
  }</pre>
または、複数のホスト名から www を削除したい場合には、ホスト名をキャッチするサーバー ブロックを追加することも可能です (注: できるだけ最初の方法をとるようお勧めします)。
<pre escaped="true">  if ($host ~* www\.(.*)) {
    set $host_without_www $1;
    rewrite ^(.*)$ $scheme://$host_without_www$1 permanent; #1
    #rewrite ^ $scheme://$host_without_www$1request_uri permanent; #2
  }</pre>
ここではホスト名に www が含まれているかどうか確認し、これを削除します。これで、次のような server 行を設けることができます。
<pre escaped="true">  server_name www.bedom.com _ ;</pre>
または次のような設定も可能です。
<pre escaped="true">  server_name domain1.com www.domain1.com domain2.com www.domain2.com ;</pre>
すべてのドメイン名をキャッチするか、一部だけをキャッチするかによって、いろいろな制御を行うことができます。また、2 番目のコメントアウトされたバージョンには URI が含まれるので、よりシームレスなユーザー体験を提供できます。

<em>メモ: </em>#1/#2 - $1 は RegEx の一部であり、かっこ内にキャッチされる部分です。if 文ではこれが 'www.' の「後」の部分であり、domain.com および #1 行では RegEx の開始 '^' と終了 '$' の間にあるすべてになります。   これはよく使われる形式ですが、2 番目のバージョンの #2 は if 文中にあるような Nginx プロセスの RegEx がないので、今の場合はこちらの方が優れています。
<h3>すべてのドメインを適切なドメインに書き換える</h3>
すべてのトラフィックをリダイレクトして適切なドメイン名を使用するようにしたい、という要請はよくあります。123.45.67.891 や ec2-123-45-67-891.compute-1.amazonaws.com を直接使用することもできますが、運用しているサイトが 1 つしかない場合、ほとんどの人はドメイン名で修正する方法を選びます。
<pre escaped="true">  server {
    listen 80 default;
    server_name _;
    rewrite ^ $scheme://www.bedom.com;
  }</pre>
その場合、他のサーバー ブロックでキャッチされないすべての要求をリッスンして、それらを http(s)://www.bedom.com にリダイレクトします。これはドメイン名に依存する今後の SSL 要求にも役立ちます。また、他のドメインに無効な URI (サイト上で一致しない URI) が含まれる可能性もあるので、通常は URI を含めません。
<h3>明らかに無効な要求のドロップ (.php/.aspx)</h3>
ときには要求が間違ったサイトに送信されることがあります。たとえば、IP アドレスの再利用、サイトの変更、構成における入力ミスといった理由から、明らかに自社のサイト宛てではない要求を着信します。通常、静的な資産を求めない要求がアプリケーションに渡されることはありません。Rails アプリケーションを実行しているということは、Active Server Pages を使用しないということであり、PHP や .CGI のファイルを実行しない可能性も高くなります。サーバー ブロックに次を追加すると、こうした要求は Rails キューに到達する前にドロップされます。
<pre escaped="true">  # Drop requests to non-rails requests
  if ($request_filename ~* \.(aspx|php|jsp|cgi)$) {
    return 410;
  }</pre>
<pre escaped="true">  # Since location blocks are usually preferred to "if"'s, this is a little better
  location ~ \.(aspx|php|jsp|cgi)$ {
    return 410;
  }</pre>
これによって、無効な要求による Rails アプリケーションの過負荷が回避されます。「次回からは試行しないように」という 410 は、404 より優れていると言えます。
<h3>いろいろな書き換えとその罠</h3>
前のセクションで、恒久的リダイレクト (ステータス 301) にはリスクが伴うと書きました。ブラウザーはこのリダイレクトを恒久的に記憶するので、注意しないと痛い目に会うことがあります。たとえば、次のような例を見かけたことがあります。
<pre escaped="true">  rewrite ^.*$ /coming_soon permanent;</pre>
これは、サイトのリニューアルに備え、すべての要求を「近日公開」ページに送るためのリダイレクトでした。最初の問題は、このコードによって coming_soon を含むすべてのページがキャッチされ、ブラウザー キャッシュ内で無限リダイレクトが発生しまったことです。これは良くありません。そこで同社は場所ブロックを使用して coming_soon の URL をキャッチしたのですが、その後 rewrite を削除して実際にリニューアルを行ったところ、リニューアル前に存在していた URL の多くが引き続き coming_soon ページにリダイレクトされていることに気付きました。permanent を使用したばかりに、同社では新しいサイトを閲覧してもらうために、お客様にキャッシュをクリアするよう依頼する結果となったのです。(実は、この問題はデプロイの直後に私が見つけたので、この問題を実際に経験したのは主に開発者とテスターだけに留まりました。)
<pre escaped="true">  rewrite ^(.*)$ https://$host$1 permanent;      #3
  rewrite ^ https://$host$request_uri permanent; #4</pre>
この 2 番目の例は、某社がそのアプリケーションで <code>ssl_requirement</code> を使用して、サイト概要や会社情報といったページを強制的に非 SSL に設定する状況で使われました。Firesheep の問題が発生した後、この行を追加してすべての要求を強制的に SSL にしたのはよかったのですが、そのときに <code>ssl_requirement</code> を更新するのを忘れたため、サイト概要ページにアクセスしたユーザーが http と https の間でバウンスされ続け、ブラウザーがタイムアウトするという事態が発生しました。

<em>メモ</em>: #3 と #4 のどちらも同じ動作をしますが、2 行目の方が Nginx の負担が軽くなります。
<h3>まとめ</h3>
この記事では、サイトで使用できる一般的なリダイレクトについて簡単に紹介しました。ドメイン名を書き換えるだけでもいろいろなオプションがあります。rewrite はパワフルで複雑な機能ですが、ごくシンプルなものでもサイト違いをもたらすことができます。
