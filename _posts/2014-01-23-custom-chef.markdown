---
layout: post
status: publish
published: true
title: Chefを拡張する3つの方法
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 2336
wordpress_url: http://www.engineyard.co.jp/blog/?p=2336
date: 2014-01-23 16:22:41.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2014/01/Chef___IT_automation_for_speed_and_awesomeness___Chef-2.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2014/01/Chef___IT_automation_for_speed_and_awesomeness___Chef-2-1024x579.png" alt="Chef___IT_automation_for_speed_and_awesomeness___Chef-2" width="1024" height="579" class="alignnone size-large wp-image-2337" /></a>

Chefを使ってサーバの管理運用をする際に作りこむ対象としてまっさきに思いつくのがクックブックです。コミュニティクックブックを組み合わせたり自作のクックブックを書くことで作り込みを行っている人は多いのではないでしょうか。しかしクックブックばかりを作りこむだけがChefを拡張する方法ではありません。

<h3>knifeプラグイン</h3>
knifeプラグインはknifeコマンドのサブコマンドを追加する形でさまざまな拡張を行う機構です。<code>knife-solo</code>もknifeプラグインの１つです。knifeプラグインはrubyを使って開発する事が出来、Amazon Web ServiceやDigital Oceanなどのパブリッククラウド環境のサポートを追加するものや、KVMやVMwareなどの仮想化環境をサポートを追加するものが多数公開されています。またコミュニティクックブックの公開や開発を支援するようなプラグインも公開されています。下記のプラグインは<a href="http://docs.opscode.com/plugin_knife.html">Chefが公式にメンテナンス</a>しているプラグインです。

<table>
<tbody><tr>
<th>名称</th>
<th>機能</th>
</tr>
<tr>
<td>knife-azure</td>
<td>Windows Azureでホストされたクラウドサーバーを管理する。同時にknife-windowsプラグインも必要になる。</td>
</tr>
<tr>
<td>knife-ec2</td>
<td>Amazon EC2でホストされたクラウドサーバーを管理する。</td>
</tr>
<tr>
<td>knife-google</td>
<td>Google Compute Engineでホストされたクラウドサーバーを管理する。</td>
</tr>
<tr><td>knife-linode</td>
<td>Linodeでホストされたクラウドサーバーを管理する。</td>

</tr><tr>
<td>knife-openstack</td>
<td>OpenStackでホストされたクラウドサーバーを管理する。</td>
</tr>
<tr>
<td>knife-rackspace</td>
<td>Rackspaceでホストされたクラウドサーバーを管理する。</td>
</tr>
</tbody></table>

上記の他にはknife-eucalyptus knife-hp knife-terremark knife-blueboxなどのプラグインがあり様々な仮想化環境のAPIへ対応する機能を提供します。

また、<a href="http://docs.opscode.com/community_plugin_knife.html">コミュニティプラグイン公式ドキュメント</a> にも50個以上のコミュニティによって作成されたプラグインがリストアップされています。コミュニティプラグインにはChef公式プラグインでサポートしない様々な仮想化環境への対応や、パブリッククラウドのAPI、Chef利用のワークフローそのものを拡張するものなど幅広いプラグインが存在します。その中でも代表的なプラグインはつぎのとおりです。

<table>
<tbody><tr>
<th>名称</th>
<th>機能</th>
</tr>
<tr>
<td>knife-solo</td>
<td>chef-solo、search、data bagsを行う為のノードの初期化(bootstrap)を行う。</td>
</tr>
<tr>
<td>knife-lastrun</td>
<td>各ノードで最後にChefを実行した際の情報を表示する。</td>
</tr>
<tr>
<td>knife-github-cookbooks</td>
<td>GitHubからクックブックをインストールする。</td>
</tr>
<tr>
<td>knife-esx</td>
<td>VMWareをサポートする。</td>
</tr>
<tr>
<td>knife-kvm</td>
<td>KVMをサポートする。</td>
</tr>
</tbody></table>

knifeプラグインはRubyGemsとして作られており、gemコマンドを使ってインストールを行います。

<pre lang="cmd">
$ /opt/chef/embedded/bin/gem install knife-azure
</pre>

標準ではChefに同梱されているgemの配下にプラグインがあるとChefクライアントはみなしています。その為、インストールしたRubyGemsが同じ場所に入るようにgemコマンドもChefに埋め込まれたコマンドを使います。gemの配置先を自分自身でコントロールしている場合は<code>/opt/chef/embedded/bin/</code>のパスを省略してインストールする事で普段使っているRuby環境と同じ場所に配置されます。

<pre lang="cmd">
$ gem install knife-azure
</pre>

上記の場合は利用しているRuby環境に見合った場所にRubyGemsがインストールされます。複数の方法を併用した場合に状況がわかりづらくなる事もあるので注意してください。特に理由がなければ開発者のPCなどワークステーションでは通常のgemコマンドを使い、実際の実行環境になるノード側ではChefに同梱されたGemを使うのが良いでしょう。

<h3>ohaiプラグイン</h3>

ノードのさまざまな情報を収集するohaiはプラグインを利用する事で独自の項目を収集し、Chef Server上に集約したり、クックブック内で参照できます。ohaiプラグインも簡単なRubyコードを記述する事で任意の処理をohai実行時に実行し結果を情報としてChefに提供できます。
ohaiのプラグインはgemなどの形にはなっていませんが、コミュニティによってさまざまなプラグインが作成されており<a href="http://docs.opscode.com/ohai.html">公式ドキュメント</a>内にリストアップされています。

<table>
<tbody><tr>
<th>プラグイン名</th>
<th>内容</th>
</tr>
<tr>
<td>dell.rb</td>
<td>サービスタグ、エクスプレスサービスコードなどのDellサーバーの有用な情報を取得する。OMSAとSMBIOSのインストールが必要。</td>
</tr>
<tr>
<td>dpkg.rb</td>
<td>Debianパッケージのdpkgの情報を取得する。</td>
</tr>
<tr>
<td>ipmi.rb</td>
<td>MACアドレスとIPアドレスを取得する。</td>
</tr>
<tr>
<td>kvm_extensions.rb</td>
<td>KVMのホストとゲストの情報を取得する。</td>
</tr>
<tr>
<td>advd.rb</td>
<td>ladvdの情報を取得する。</td>
</tr>
<tr>
<td>lxc_virtualization.rb</td>
<td>LXCのホストとゲストの情報を取得する。</td>
</tr>
<tr>
<td>network_addr.rb</td>
<td>ネットワークインターフェースの情報を扱いやすく拡張する。</td>
</tr>
<tr>
<td>network_ports.rb</td>
<td>各ネットワークインターフェースのTCPとUDPの状況を取得する。</td>
</tr>
<tr>
<td>parse_host_plugin.rb</td>
<td>ホスト名を3段階、5段階でパースする。</td>
</tr>
<tr>
<td>r.rb</td>
<td>Rプロジェクトに関する情報を取得する。</td>
</tr>
<tr>
<td>rpm.rb</td>
<td>RPMパッケージマネージャーの情報を取得する。</td>
</tr>
<tr>
<td>sysctl.rb</td>
<td>sysctlの情報を取得する。</td>
</tr>
<tr>
<td>vserver.rb</td>
<td>Linux VServerの情報を取得する。</td>
</tr>
<tr>
<td>wtf.rb</td>
<td>wtfismyip.com を使ってホストの外部IPアドレスと地理情報を取得する。</td>
</tr>
<tr>
<td>xenserver.rb</td>
<td>Citrix XenServerのホストとゲストの情報を取得する。</td>
</tr>
<tr>
<td>win32_software.rb</td>
<td>Windows Management Instrumentation (WMI)を使いWindowsノード上にインストールされたソフトウェアの情報を取得する。</td>
</tr>
<tr>
<td>win32_svc.rb</td>
<td>Windows Management Instrumentation (WMI)を使いWindowsノード上で稼働するサービスの情報を取得する。</td>
</tr>
</tbody></table>

<h3>chefプラグイン</h3>
knifeやohaiではなくChefクライアントの実行時の挙動を拡張するプラグインもRubyGemsとして公開されています。<a href="http://docs.opscode.com/community_plugin_chef.html">公式ドキュメント</a>にリストアップされている以外のRubyGemsも日々公開されていますので用途にあったものがあれば導入したり、拡張するのがよいでしょう。

<table>
<tbody><tr>
<th>プラグイン名</th>
<th>内容</th>
</tr>
<tr>
<td>chef-deploy</td>
<td>Rubyアプリケーションのデプロイを行うリソースとプロバイダを追加する。</td>
</tr>
<tr>
<td>
chef-gelf</td>
<td>Graylog2サーバーへの通知を行う。</td>
</tr>
<tr>
<td>chef-handler-twitter</td>
<td>ツイートを行うハンドラーを追加する。</td>
</tr>
<tr>
<td>chef-handler-librato</td>
<td>Libratoへ統計情報を送信する。</td>
</tr>
<tr>
<td>chef-hatch-repo</td>
<td>サーバーを仮想マシンやAmazon EC2へ起動するVagrantプロビジョナーを追加するknifeプラグイン。</td>
</tr>
<tr>
<td>chef-irc-snitch</td>
<td>chefクライアント実行時の例外をIRCに通知する。</td>
</tr>
<tr>
<td>chef-jenkins</td>
<td>Jenkinsを利用した継続的なデプロイをGitリポジトリから行う。</td>
</tr>
<tr>
<td>chef-rundeck</td>
<td>Rundeckのリソースエンドポイントを追加する。</td>
</tr>
<tr>
<td>chef-solo-search</td>
<td>chef-soloでもdata-bagやenvironmentへの検索を行う。</td>
</tr>
<tr>
<td>chef-trac-hacks</td>
<td>AWSとchefクライアントの間の差を埋める。</td>
</tr>
<tr>
<td>chef-vim</td>
<td>クックブックのナビゲーションを素早く行う。</td>
</tr>
<tr>
<td>chef-vpc-toolkit</td>
<td>仮想サーバーのグループを管理するRakeタスクを追加する。</td>
</tr>
<tr>
<td>
ironfan</td>
<td>スケーラブルなクラスタの構築と設定を補助する。</td>
</tr>
<tr>
<td>jclouds-chef</td>
<td>Chef SeverのRest APIへのJavaとClojureのコンポーネントを追加する。</td>
</tr>
</tbody></table>

<h3>もちろん自作も可能</h3>
knifeプラグイン、ohaiプラグイン、chefプラグインのいずれも自作できます。コミュニティで公開されているプラグインの内容は公式ドキュメントの内容を参考にすればChefの細かな挙動をカスタマイズし、よりスムーズな運用ができるでしょう。

<ul>
<li><a href="http://docs.opscode.com/plugin_knife_custom.html">Custom Knife Plugins — Chef Docs</a></li>
<li><a href="http://docs.opscode.com/ohai.html#custom-plugins">About Ohai — Chef Docs</a></li>
</ul>

<hr/>
<a href="http://ey.io/noyakshave"><img src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png"></a>
