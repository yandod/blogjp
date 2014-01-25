---
layout: post
status: publish
published: true
title: Chefのレシピは上から下に実行されるという誤解
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1965
wordpress_url: http://www.engineyard.co.jp/blog/?p=1965
date: 2013-11-28 17:12:40.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/名称未設定-300x254.png" alt="名称未設定" width="300" height="254" class="alignnone size-medium wp-image-1989" />

Engine Yardを含むさまざまな場面で利用が広がったChefですが、その動作原理やアーキテクチャについてご存じない方もいることに気が付きました。細かなアーキテクチャを理解しなくても使うことができるというChefの長所を示しているともいえますが、細かな挙動を制御する際にはやはり動作原理などの知識があると役立ちます。
今回は表題のとおりレシピが実行される際のサイクルについてあまり知られていない部分を紹介します。


<h3>Chefの実行サイクルとリソースコレクション</h3>

Chef(Chef Client、Chef Solo)が実行された際には直ちにサーバの設定が始まるわけではなく、さまざまなステップ毎に処理が実行されます。大まかには下記のようなステップになります。

<ol>
	<li>Chef Serverとの通信、認証処理</li>
	<li>Chef Serverからのクックブック、データの取得</li>
	<li>クックブックのコンパイル</li>
	<li>ノードの設定、収束(Converge)</li>
	<li>通知(Notification)の実行</li>
</ol>

上記の内、最初の2つはChef Soloの場合は存在しないか、その他のツールを使って自力で済ませる事になります。ここでポイントになるのが3つ目のクックブックのコンパイルです。クックブックはRubyで書かれたレシピの集合体です。レシピの中ではChefが提供するリソースという仕組みを使ってサーバへのパッケージの導入や設定ファイルの操作などを行います。例えば下記の例では<code>execute</code>リソースや<code>package</code>リソース、<code>service</code>リソースなどを使ってvimのインストールやデーモンの再起動を行っている例です。また合間合間でデバッグ用のメッセージを出力しています。

<pre lang="ruby">
p "One"
execute "apt-get update" do
  action :run
end

p "Two"
package "vim" do
  action :install
end

p "Three"
service "ssh" do
  action :restart
end
</pre>

上記のレシピは実行時にそれぞれのリソース部分が対応するオブジェクトに変換されコレクションに格納して<code>Converge</code>のフェーズまで保持されます。つまり利用する全てのクックブック内で使ったリソースがコレクションに格納されるまで実際のサーバの設定作業は一切開始されない点に注意してください。実際の実行ログを見ると、下記のようにデバッグ用の出力は実際のリソースの実行よりも先になっています。

<pre lang="cmd">
INFO: *** Chef 10.14.2 ***
WARN: Run List override has been provided.
WARN: Original Run List: []
WARN: Overridden Run List: [recipe[scott]]
INFO: Run List is [recipe[scott]]
INFO: Run List expands to [scott]
INFO: Starting Chef Run for precise64
INFO: Running start handlers
INFO: Start handlers complete.
"One"
"Two"
"Three"
INFO: Processing execute[apt-get update] action run (scott::default line 10)
INFO: execute[apt-get update] ran successfully
INFO: Processing package[vim] action install (scott::default line 15)
INFO: Processing service[ssh] action restart (scott::default line 20)
INFO: service[ssh] restarted
INFO: Chef Run complete in 6.449472 seconds
Running report handlers
INFO: Report handlers complete
</pre>

リソースの処理を直ちに実行させる必要がある場合はコンパイルされたオブジェクトを操作する下記のような記述も出来ます。

<pre lang="ruby">
e = execute "apt-get update" do
  action :nothing
end

e.run_action(:run)
</pre>

<strong>追記</strong>
リソースコレクションの中のオブジェクトは<code>resources</code>メソッドで取得できます。下記の例ではどこかで定義されたFileリソースの設定を後から変更しています。

<pre lang="ruby">
f = resources("file[/etc/hosts]")
f.mode 00644
</pre>

<h3>Rubyスクリプトはコンパイル時に実行される</h3>
次に注意すべき点がレシピ内に書かれたRubyスクリプトの部分はコンパイル時に実行されるという点です。先ほども触れたようにリソースの実際の処理はコンパイル時ではなく収束(Converge)の際に行われますので、Rubyスクリプトの部分でリソースの実行によって起きた変化を前提とするような処理はできません。

<pre lang="ruby">
file "/var/hoge4" do
  action :create
end

#コンパイルの時点ではファイルは作成されていない
if !File.exist?("/var/hoge4") then
  p "File not found"
end
</pre>

しかもこの上記の例は2回目以降の実行では前回実行時にファイルが作成されている為、挙動が変わります。条件比較の記述ミスなどが重なると何が起きているかを誤解する可能性の高い状況になりますので注意が必要です。
Rubyのスクリプトによる処理をコンパイル時ではなく収束時に行いたい場合は<code>ruby_block</code>リソースを使います。

<pre lang="ruby">
file "/var/hoge5" do
  action :create
end

#リソースとして実行されればはファイルは作成されている
ruby_block "check_file" do
  block do if File.exist?("/var/hoge5") then
      p "found"
    end
  end
end
</pre>

そのままRubyを記述できるのに、なぜこのようなリソースが存在するのかがお分かり頂けたでしょうか？もちろんこのリソースもリソースコレクションに格納されるので別のレシピなどから挙動に関与する事も可能です。Rubyスクリプトの実行タイミングを遅らせたい場合にはこの方法が必要になります。

<h3>通知(Notification)を使っていますか？</h3>
次に注意したいのが収束(Converge)の後に行われる通知の実行です。設定ファイルなどが変更された際はサービスの再起動が必要になります。そういった際は設定ファイルの変更が行われる処理の後にサービスの再起動などを記述するでしょう。しかし関連する設定ファイルが複数あったり、複数のレシピから変更されている場合はどうでしょうか？
単純に記述してしまうと、一回のChefの実行で何度も同じサービスが再起動されてしまいますが、通知を使うことで全ての設定作業が終わった後にまとめてサービスの再起動を行うような記述が出来ます。

通知として実行されたいリソースにはアクションとして:nothingを設定します。そして設定ファイルなどを変更するリソースから<code>notifies</code>アトリビュートを使ってアクションやリソースコレクション名、タイミングを指定します。
下記の例では<code>file</code>リソースを使って2つのファイルを作成し、1つのリソースからはsshサービスの再起動を行っています。

<pre lang="ruby">
service "ssh" do
  action :nothing
end

file "/var/hoge" do
  action :create
  notifies :restart, "service[ssh]", :delayed
end

file "/var/hoge2" do
  action :create
end
</pre>

上記のレシピは記述の順番と実行の順が異なり、sshの再起動は最後になっている事がログで確認出来ます。

<pre lang="cmd">
INFO: *** Chef 10.14.2 ***
WARN: Run List override has been provided.
WARN: Original Run List: []
WARN: Overridden Run List: [recipe[scott]]
INFO: Run List is [recipe[scott]]
INFO: Run List expands to [scott]
INFO: Starting Chef Run for precise64
INFO: Running start handlers
INFO: Start handlers complete.
INFO: Processing service[ssh] action nothing (scott::default line 10)
INFO: Processing file[/var/hoge] action create (scott::default line 14)
INFO: file[/var/hoge] created file /var/hoge
INFO: Processing file[/var/hoge2] action create (scott::default line 19)
INFO: file[/var/hoge2] created file /var/hoge2
INFO: file[/var/hoge] sending restart action to service[ssh] (delayed)
INFO: Processing service[ssh] action restart (scott::default line 10)
INFO: service[ssh] restarted
INFO: Chef Run complete in 1.332552 seconds
INFO: Running report handlers
INFO: Report handlers complete
</pre>

<h3>まとめ</h3>
なんとなく記述すれば動作するのはChefの利点ですが、実行サイクルを理解する事で意図しない挙動や冪等性のないレシピになってしまう状況を防ぐ事ができます。
特に実行順などを制御する方法は数多くのレシピを組み合わせる際などに有用ですので是非覚えておきましょう。

<h3>おまけ：Chefに関する情報源</h3>
ブログ記事などが多く見つかる状況ですが、取りまとめられたコンテンツもあります。特に下記のコンテンツは量も豊富かつ正確なので参照するとよいでしょう。

<ul>
<li>「初めてのChefの教室」を開催しました。(動画&資料) | Engine Yard Blog JP
<a href="http://www.engineyard.co.jp/blog/2013/engineyard-meetup-chef-seminar/" target="_blank">http://www.engineyard.co.jp/blog/2013/engineyard-meetup-chef-seminar/</a></li>
<li>Rubyist Magazine - Chef でサーバ管理を楽チンにしよう！ (第 1 回)
<a href="http://magazine.rubyist.net/?0035-ChefInDECOLOG" target="_blank">http://magazine.rubyist.net/?0035-ChefInDECOLOG</a></li>
<li>Opscode Open Source Wiki(情報が古いが日本語の情報)
<a href="https://wiki.opscode.com/pages/viewpage.action?pageId=24019581" target="_blank">https://wiki.opscode.com/pages/viewpage.action?pageId=24019581</a></li>
<li>Chefについてのドキュメント(英語)
<a href="http://docs.opscode.com/" target="_blank">http://docs.opscode.com/</a></li>
<li>Resources and Providers Reference — Chef 
<a href="http://docs.opscode.com/chef/resources.html" target="_blank">http://docs.opscode.com/chef/resources.html</a></li>
<li>Recipe DSL — Chef 
<a href="http://docs.opscode.com/chef/dsl_recipe.html" target="_blank">http://docs.opscode.com/chef/dsl_recipe.html</a></li>
<li>Esseintials nodes chef run
<a href="http://docs.opscode.com/essentials_nodes_chef_run.html" target="_blank">http://docs.opscode.com/essentials_nodes_chef_run.html</a></li>
</ul>

<strong>[PR] Engine YardのPaaSを利用すればChefを使った運用の強力にサポート。クックブックのコンサルティングも提供しています。</strong>
<div><a href="http://ey.io/noyakshave"><img class="alignnone size-full wp-image-1889" style="border: 1px solid black;" alt="noyakshave_seminar_small" src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png" /></a></div>
