---
layout: post
status: publish
published: true
title: Zend Framework作者によるEngine YardへのPHPアプリのデプロイハウツー (翻訳版)
author: Matthew Weier O'Phinney
author_login: matthewweier
author_email: yando+matthewweier@engineyard.com
wordpress_id: 1504
wordpress_url: http://www.engineyard.co.jp/blog/?p=1504
date: 2013-09-30 12:58:46.000000000 +09:00
categories:
- Uncategorized
tags:
- 技術情報
- PHP
comments:
- id: 69
  author: Satoru Yoshida
  author_email: ramat@ram.ne.jp
  author_url: ''
  date: '2013-10-01 06:37:00 +0900'
  date_gmt: '2013-09-30 21:37:00 +0900'
  content: 正しくは、「Zend Framework プロジェクトのリーダー」とすべきでしょうね。彼一人だけで作ったものではありませんので
- id: 70
  author: Yusuke Ando
  author_email: yando@engineyard.com
  author_url: ''
  date: '2013-10-03 13:01:00 +0900'
  date_gmt: '2013-10-03 04:01:00 +0900'
  content: そうですね。ただまぁ最近のOSS何でもそうですね。冒頭のプロフィールにはリードである旨は書いてありますので、あくまで見出しを短くする為の表現と理解して頂ければ。
- id: 71
  author: Satoru Yoshida
  author_email: ramat@ram.ne.jp
  author_url: ''
  date: '2013-10-06 19:47:00 +0900'
  date_gmt: '2013-10-06 10:47:00 +0900'
  content: 確かに見出しは長くなってしまいますね。了解しました
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/名称未設定-2.jpg" alt="名称未設定-2" width="863" height="471" class="alignnone size-full wp-image-1600" />
<div class="note">
<a href="https://github.com/weierophinney" target="_blank">Matthew Weier O'Phinney氏</a>はZend Frameworkのプロジェクトリードとして知られる、PHPコミュニティの中でも特に大きな業績があり、また広いネットワークを持っている人物です。今回、Matthew氏がゲスト投稿としてEngine Yardのブログに寄稿して頂きました。本記事は英語版のブログで<a href="https://blog.engineyard.com/2013/deploying-php-applications-on-engine-yard-a-how-to" target="_blank">2013/09/25に公開された記事</a>の翻訳版です。
</div>

私は最近、様々なクラウド プラットフォーム サービス(PaaS)の試験をしていて、ごく自然にEngine YardがPHP開発者の為に提供する<a href="http://www.engineyard.co.jp/products/cloud" target="_blank">Engine Yard Cloud</a>に興味を持つようになった。

筆者のアプリケーションのデプロイは、いくつかの非自明な側面が含まれており、それを実現する事が簡単だったり、難しかったりするかを知りたかった。これには下記のようなものを含む。：

<ul>
<li>Gitリポジトリからデプロイ。</li>
<li>私のプロジェクトのリポジトリ内でGitのサブモジュールの使い方。</li>
<li>サードパーティのコードの主な依存関係管理のためのComposerの使い方。</li>
<li>APIキーのようなものを含むいくつかのプライベートコンフィギュレーションファイルの扱い。(これらはプライベートGitHubのリポジトリに格納されています。)</li>
<li>Webサービスを介して情報を収集するためのいくつかの "実行前"の作業。</li>
<li>いくつかのcronジョブ。</li>
<li>準備ができたらホームページを解決するためのDNS。</li>
</ul>

Engine Yardのスタックはどんな具合でしょうか？これら、全てのタスクを実行することができるでしょうか？

後者の質問への答えは「イエス」です。前者の質問への答えは「非常に良い。」となります。

<h3>初期のデプロイ: Git と Composer</h3>

最初にEngine Yardでアプリケーションを作成する場合、既存のGitリポジトリのURLを指定するように求められます。 Engine Yardは、このリポジトリをクローニングすることにより、アプリケーションをデプロイします。必要に応じてブランチ、タグ、またはEngine Yardが使用する特定のリビジョンを指定することができます。

さらに、デフォルトでリポジトリを再帰的にクローンしており(i.e., <code>git clone&nbsp;--recursive</code>)、あなたが任意のサブモジュールを持っている場合、これらは自動的に同様にクローンされることを意味します！これは私が他のプロダクトを試した際に見られなかった機能でした。（他のPaaSソリューションでは、私のデプロイの一部として手動でのサブモジュールの初期化しなければならない事が多かった）このおかげで初期のデプロイはとても簡単です。

Engine Yardは、PHPプロジェクトのルートに<code>composer.lock</code>ファイルを検出した場合、直ちに依存関係管理ツール Composerをインストールし、<code>composer install</code>を実行します。これによりデプロイは非常に簡素化されます。依存するライブラリをパッケージにしてそれぞれプッシュしたり、依存関係をインストールするデプロイタスクを作成する必要はありません。Engine Yardがあなたの面倒な仕事を手助けします。

注：今現在、私はComposerが<code>--no-dev</code>フラグ付きでの実行を考慮しているかを問い合わせています。デフォルトの "development"モードで実行された場合、あなたは<code>composer.lock</code>ファイルの内容について慎重であるべきです。実行中のバージョンのチェックは<code>--no-dev</code>のフラグが指定された時のみ行われます。

<h3>プライベートな設定</h3>

次のアジェンダは筆者のプライベートな設定ファイルをどのようにして環境に設置するかです。

Zend Framework 2は、全ての環境で利用可能なグローバル設定とAPIキーやデータベースの接続情報などを持ちバージョンコントロールにチェックインされる事のないローカル設定を<code>glob</code>パスを使ってマージします。実行時設定は、ローカルがグローバルに優先する形で、グローバルおよびローカル設定がマージされた結果です。

私は伝統的に大体このような形でデプロイを行ってきた:

- センシティブなローカル設定の為のプライベートな git リポジトリを作成。
- デプロイ中に：
- tempディレクトリ内にプライベートリポジトリをクローン。
- 設定ファイルを私のアプリにコピー。

このアプローチの問題は、もちろん、あなたのサーバーにSSH鍵を設定し、GitHubのまたは他のGitのホスティングプラットフォーム上のキーリングにそれらを追加する必要があることです。クラウドプラットフォームでは、これは、問題となる可能性があります。サーバーは起動する度に異なるサーバーになる為、SSHがman-in-the-middle (MitM) 攻撃と誤認され、サーバーがリポジトリにアクセスできなくなります。

さらに、新たな疑問が発生します：サーバはどこからどのようにしてSSH鍵を取得するのでしょうか？

Engine Yardは、アプリケーションコンテナを管理し、構成するためにChefを使用しています。新しいアプリケーションを作成すると、デフォルトの設定を使用します。ただし、ローカルでその構成をチェックアウトし、レシピを追加または変更すると、新しい設定をプッシュすることができます！

これができれば、SSHキーについて悩む必要もありません。アプリケーションがデプロイされたときに、我々はシンプルにコンテナに我々のファイルをプッシュすることができます。

始めるには、まず<a href="http://rubygems.org/gems/engineyard" title="Engine Yard Gem" target="_blank">Engine YardのRuby gem</a>をインストールする必要があります。

<pre lang="cmd">
$ gem install engineyard
</pre>

PHP用のベースになるレシピはここにあります。:
- <a href="https://github.com/engineyard/ey-cloud-recipes-chef-10.git" title="engineyard/ey-cloud-recipes-chef-10" target="_blank">https://github.com/engineyard/ey-cloud-recipes-chef-10.git</a>

ローカルでそのリポジトリを（<code>git clone https://github.com/engineyard/ey-cloud-recipes-chef-10.git</code>）クローンするだけで、編集を始められます。私ZF2ベースのアプリケーションのために、私はディレクトリ <code>cookbooks/php/files/default/</code> を作成し、その中に私の各種 <code>*local.php</code> ファイルをコピーしました。その後、<code>cookbooks/php/recipes/production_config.rb</code>のChefのレシピを作成し、そのクックブックでこれらのファイルを<code>shared/appconfig</code>をコピーしてアプリケーションコンテナのどこからでも読み込めるようにしました。

<pre lang="ruby">
ey_cloud_report "production_config" do
   message "Production config pushed"
end
 
directory "/data/myappname/shared/appconfig" do
    owner node[:owner_name]
    group node[:owner_name]
    mode 0755
    action :create
end
 
[
    'database.local.php',
    'local.php',
    'module.application.local.php',
    'module.blog.local.php',
    'module.github-feed.local.php',
    'module.phly-contact.local.php',
    'scn-social-auth.local.php'
].each do |config|
    cookbook_file "/data/myappname/shared/appconfig/#{config}" do
        owner node[:owner_name]
        group node[:owner_name]
        mode 0644
        source "#{config}"
        backup false
        action :create
    end
end
</pre>

注：Chefのレシピは、私が多くの経験を持ってない言語、Rubyで書かれています。ファイルをメンテナンスしやすくするより簡単な方法があれば、私に知らせてください！

レシピが作成されましたので、私はそれを使用するためにChefを指示する必要があります。次のファイル <code>cookbooks/main/recipes/default.rb</code> を編集して次の行を追加します。

<pre lang="ruby">
include_recipe "php::production_config"
</pre>

クローンしたChefのレシピリポジトリのルートから、Engine Yard gemを使用してレシピをデプロイします。

<pre lang="cmd">
$ ey recipes upload -e ENV
</pre>

<code>ENV</code> は、アプリケーションの対象になる環境です。上記の私のChefのレシピ例では、それは "本番"に対応する。これらのファイルのいずれかに変更を加えるたびに、あなたのコンテナに変更をデプロイするために、そのコマンドを再発行します。

Webインターフェイスでアプリケーションの画面を見ると、コンテナが「Custom recipes uploaded」のメッセージを表示しているのが確認できます。

<a href="https://blog.engineyard.com/wp-content/uploads/chef-uploaded.png"><img class="alignnone size-full wp-image-15085" alt="chef-uploaded" src="https://blog.engineyard.com/wp-content/uploads/chef-uploaded.png" width="629" height="236"></a>


レシピを実行するには、それぞれの環境の画面で、"Apply"をクリックするか、またはengineyard gemを使う事ができます。

<pre lang="cmd">
$ ey recipes apply -e ENV
</pre>

<h3>デプロイタスク</h3>

あなたは、私が設定ファイルをアプリケーションの中ではなく、共有ディレクトリ(<code>/data/myappname/shared</code>)に入れたことに気づいたかもしれません。これはコンテナの作成直後に、アプリケーションがまだデプロイされていない場合があるからです。

では、アプリケーションはどのようにそれらのファイルを見ればいいのでしょうか？
答えは、いくつかのデプロイスクリプトを追加することです。

Engine Yardは各種のデプロイフックをサポートしています。あなたのアプリケーションの<code>deploy/</code>以下にあるそれぞれのフックに対応したスクリプトが存在していれば、実行されます。スクリプトはRubyで記述されており。シンプルな共通の処理についてはいくつかの文法が存在しています。

- <code>run</code> と <code>sudo</code> コマンドを使用すると、任意のシェルコマンドを実行できるようになります。どちらかの後に感嘆符（"!"）を使用すると、コマンドが失敗した際にデプロイをエラーとして中断できます。例) <code>run! someCommand</code>, <code>sudo!&nbsp;someCommand</code>

- 上記のコマンドは、ファイルシステムレイアウトの特定の詳細を知る必要がないように、いくつかの環境変数を利用できます。具体的には、<code>#{shared_path}</code> と <code>#{release_path}</code> 変数が便利です。

- 実行可能なPHPは <code>/usr/bin/php</code> にあり、常に利用できます。

つまり、 <code>deploy/before_symlink.rb</code> にスクリプトを作成し、下記のようにする事でローカル設定ファイルをコピーできるという事になります。:

<pre lang="ruby">
run "cp #{shared_path}/appconfig/*.php #{release_path}/config/autoload/"
</pre>

上記のコマンドが失敗した時、処理を中断したい場合は次のように書きます。:

<pre lang="ruby">
run! "cp #{shared_path}/appconfig/*.php #{release_path}/config/autoload/"
</pre>

この時点で、他に実行したいタスクがなければ、私のアプリケーションのプロダクション用の設定が設置され、私のアプリケーションの準備が完了しました！
今回、私は展開するときに実行したいいくつかのタスクがあり、これらはZF2のコンソールツールを使用して書かれています。よって、私は上記のスクリプトには、さらにいくつかの行を追加しました：

<pre lang="ruby">
run "cd #{release_path} && /usr/bin/php public/index.php githubfeed fetch"
run "cd #{release_path} && /usr/bin/php public/index.php phlysimplepage cache clear all"
</pre>

上記の各リリースパスに入った後、PHPバイナリを使用してZF2 consoleコマンドを実行します。
うまくいっているようです！

<blockquote><p>注: Engine Yardがサポートする全てのフックがPHPアプリケーションで利用できるわけではありません。下記のフックは <strong>実行されません。</strong> <code>before_compile_assets.rb</code>, <code>after_compile_assets.rb</code>, <code>before_migrate.rb</code>, <code>after_migrate.rb</code>. その他のフックは利用可能です。私は、<code>before_symlink.rb</code> が私の全てのデプロイタスクを実行するのに適している事に気が付きました。</p></blockquote>

<h3>Cronジョブ</h3>

私は定期的に実行するいくつかのタスクを持っています。例えば、サイトはいくつかのGitHubの統計を時間ごとに更新する必要があります。これらはcronジョブに最適です。
Engine Yardははcronジョブを設定するためのWebインターフェイスを提供します。このインタフェースは、基本的には様々な間隔、次に実行するタスクを指定することができるように、crontabエントリを模しています。

<a href="https://blog.engineyard.com/wp-content/uploads/cronjob.png"><img class="alignnone  wp-image-15086" alt="cronjob" src="https://blog.engineyard.com/wp-content/uploads/cronjob.png" width="501" height="228"></a>

あなたは、アプリケーション自体の内部でタスクを実行したい場合は、1つの潜在的な問題がある。デプロイフックでは、前のセクションで見たように、我々はパスを解決する環境変数にアクセスすることができます。しかし、cronジョブではどうすればいいでしょうか？
Engine Yardは、アプリケーションをデプロイする際にシンボリックリンクを使用しています。シンボリックリンクを、問題なく動作していた以前のデプロイ先に単純にポイントしなおすという、簡単でスマートなロールバックを行うことができます。副次的な利点は、現在のアプリケーションが常に同じ場所で利用可能であることを意味するということです：
 <code>/data/&lt;your app name&gt;/current</code>.

例えば、私のあるcronジョブは、以下を実行します。

<pre lang="cmd">
$ cd /data/myappname/current && /usr/bin/php public/index.php githubfeed fetch
</pre>

私のcronジョブの設定は数分で全て終わりました。

<h3>DNS</h3>

現在、私はアプリケーション環境を持ち、そしてそれを実行しています。では、どのようにしてこのアプリケーションにアクセスできるのでしょうか？

Engine YardはAmazon AWS Elastic IP アドレスを使用し、各アプリケーションに Elastic IPを関連付けます。あなたのEngine Yardコンテナは別のマシンに移動した場合、AWSはまだそれを見つけることができることを意味します - これらのアドレスは、AWSアカウントではなく、特定のマシンに関連付けられています。
あなたのコンテナを作成するときは、作成済のIPアドレスを関連付けるか、新たにIPアドレスを作成して関連づけるかのを確認していたでしょう。

いくつかの他のPaaSプラットフォームでは、"裸のドメイン"と呼ばれるものを持つことができず、サブドメインを使用する必要があります。実際に、<a href="http://wwwizer.com/naked-domain-redirect" title="wwwizer.com" target="_blank">wwwizer</a>などのサービスは、"www"サブドメインに裸のドメインをリダイレクトして、この問題を解決するために存在しています。もちろんこれは、新たな問題を提示し、裸のドメインへのそれぞれすべてのコールがリダイレクトされます。

Elastic IPを使用する方法について興味深いのは、DNSのAレコードを持っているように、あなたのクラウド·アプリケーションとの裸のドメインを使用できることです。

<h3>結論</h3>

Engine Yardは、非常に上手に、いくつかの一般的なデプロイの問題に対して柔軟性の高いPaaSのソリューションを提供します。あなたが最初に目にするGitとComposerを使用してデフォルトのデプロイは、ほとんどのアプリケーションのデプロイに関連する作業の大部分を魔法のように解決します。Chefの使用は、デプロイよりも複雑であったりセンシティブな部分を、ドキュメントとノウハウが抱負なツールを使用して管理できることを意味します。デプロイフックスクリプトは、アプリケーションを動作させる前に準備し、設定し、キャッシュを生成するといった事を出来るようにします。cronジョブが使用可能ということは、デフォルトで非同期処理の機能を提供します。最後に、Elastic IPの使用は、あなたの裸のドメインを使って、クラウドでホストできることになります。

私は非常に実験に満足しています。私の経験は他のPHP開発者がクラウドアプリケーションのデプロイをテストする際の助けになることを願っています。

<h3>謝辞</h3>
Davey Shafik は私のデプロイについての初期の質問を受け最終的にはそれらに全て答えることができませんでしたが、全てがうまくいったらこの記事を書くように促してくれました。
Kevin Holler はデプロイの際に利用できるフックスクリプトについての情報を示してくれました。また更に重要な事にどのフックがPHPアプリケーションで利用できるかについても。
最後にEngine YardのサポートチームはプライベートなファイルについてEngine Yardが標準で利用するPHPレシピと同様にChefが解決策になる事を示してくれました。

<hr>
Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。PHPを利用したアプリケーションをデプロイする際は、Engine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/trial"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>
