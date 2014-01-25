---
layout: post
status: publish
published: true
title: Puppet でインフラストラクチャを管理する理由 (翻訳版)
author: curtmichol
author_login: curtmichol
author_email: curtmichol@engineyard.com
excerpt: "<div class=\"note\">\r\n本記事は<a href=\"http://blog.engineyard.com/2011/why-puppet-should-manage-your-infrastructure\"
  target=\"_blank\">英語版のブログに2011年3月7日</a>に投稿された記事の翻訳版です。\r\n</div>\r\n\r\nいかにシンプルなインフラストラクチャでも、そのセットアップと保守を自動化する場合、通常は、一般的な設定管理ツールである
  <a href=\"http://puppetlabs.com/\">Puppet</a> と <a href=\"http://opscode.com/\">Chef</a>
  のどちらかの使用を決めることになるのが現状です。<a href=\"http://www.cfengine.org/\">他の</a><a href=\"http://trac.mcs.anl.gov/projects/bcfg2\">ツール</a>もあり、ものによってはかなり以前から公開されてます。しかし、最近は
  Puppet と Chef の開発ペースが速まっており、両者が急成長していることを示しています。\r\n\r\nこの記事は、Puppet を使ってインフラストラクチャを管理するいくつかの利点の説明から始めたいと思います。<a
  href=\"http://www.engineyard.com/blog/2011/why-chef-should-manage-deploying-your-application/\">Chef
  の概要</a>と、その独自の機能がインフラストラクチャにどのようなメリットをもたらすかについても、近日中に取り上げる予定です。\r\n<h3>インフラストラクチャを管理可能なコンポーネントに分解する</h3>\r\nインフラストラクチャは比較的複雑となり得ますが、特定のアプリケーションをサポートするためコンポーネントを追加していくうちに、ますます複雑なものとなります。しかし、インフラストラクチャの設定をすべて個々のコンポーネントに分解して、インストール、設定、および監視を行うことができます。これらのコンポーネントは、1
  人のユーザーや 1 つのファイルのようにシンプルな場合もあれば、バックエンド データをサポートするクラスター内の複数のサーバーのように複雑な場合もあります。\r\n\r\n"
wordpress_id: 641
wordpress_url: http://www.engineyard.co.jp/blog/?p=641
date: 2013-03-21 10:00:22.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">
本記事は<a href="http://blog.engineyard.com/2011/why-puppet-should-manage-your-infrastructure" target="_blank">英語版のブログに2011年3月7日</a>に投稿された記事の翻訳版です。
</div>

いかにシンプルなインフラストラクチャでも、そのセットアップと保守を自動化する場合、通常は、一般的な設定管理ツールである <a href="http://puppetlabs.com/">Puppet</a> と <a href="http://opscode.com/">Chef</a> のどちらかの使用を決めることになるのが現状です。<a href="http://www.cfengine.org/">他の</a><a href="http://trac.mcs.anl.gov/projects/bcfg2">ツール</a>もあり、ものによってはかなり以前から公開されてます。しかし、最近は Puppet と Chef の開発ペースが速まっており、両者が急成長していることを示しています。

この記事は、Puppet を使ってインフラストラクチャを管理するいくつかの利点の説明から始めたいと思います。<a href="http://www.engineyard.com/blog/2011/why-chef-should-manage-deploying-your-application/">Chef の概要</a>と、その独自の機能がインフラストラクチャにどのようなメリットをもたらすかについても、近日中に取り上げる予定です。
<h3>インフラストラクチャを管理可能なコンポーネントに分解する</h3>
インフラストラクチャは比較的複雑となり得ますが、特定のアプリケーションをサポートするためコンポーネントを追加していくうちに、ますます複雑なものとなります。しかし、インフラストラクチャの設定をすべて個々のコンポーネントに分解して、インストール、設定、および監視を行うことができます。これらのコンポーネントは、1 人のユーザーや 1 つのファイルのようにシンプルな場合もあれば、バックエンド データをサポートするクラスター内の複数のサーバーのように複雑な場合もあります。

<a id="more"></a><a id="more-641"></a>設定管理ツールを使用するには、こうした個々の要素とその関係を考慮する必要があります。サーバー間の関係や、サーバーを構成する個々のコンポーネントの間の関係がその対象となります。

たとえば、Ruby on Rails アプリケーションのデプロイには、通常はデータベース、アプリケーション サーバー、およびウェブ サーバーが必要です。これらは単一のマシンに設定できますが、複数のマシンに分解してマシンごとにコンポーネントを設定することも可能です。このような要素間の関係を考え、それをサポートするインフラストラクチャを開発することで、各コンポーネントを商品として扱い、それぞれを一貫した方法で容易に追加、削除、または置換できるようになります。
<h3>Puppet リソースの概要</h3>
Puppet ではこうしたコンポーネントのことを "リソース" と呼んでいます。Puppet のリソースにはタイプ、名前、そしてリソースの設定を定義する属性があります。次にリソースの例を示します。
<pre escaped="true">file { "/etc/ntp.conf":
    owner =&gt; root,
    group =&gt; root,
    mode =&gt; 0644,
    source =&gt; "puppet:///ntpd/ntp.conf"
}
</pre>
一般にリソースはそのタイプで始まり (ここでは "file" タイプを使用しています)、その後にリソースの名前と属性を中かっこで囲みます。この例ではリソースの "名前" が "/etc/ntp.conf" で、その後にコロンが続きます。このコロンと閉じ中かっこの間にあるのは、すべてリソースの属性です。

このリソースは、インフラストラクチャのコンポーネントである、"/etc/ntp.conf" にあるファイルを管理します。また、このファイルの所有者を "root" とし、許可が "0644" であることも指定されています。このリソースの実行用に選択する任意のノードに、これらの属性が設定されたファイルが設けられます。
<h3>リソース間の関係の定義</h3>
他のツールにはない Puppet の特長として、こうしたリソースと、それが定義されているモジュールとの間の関係を指定できる点が挙げられます。ここでモジュールとは一般に、インストール、設定、監視の 3 つのコア要件の 1 つを含む設定として考えられます。Puppet のモジュールは通常はクラスに分解され、クラスは<a href="http://docs.puppetlabs.com/guides/language_tutorial.html">リソース</a>のシングルトンなコレクションです。

前例を続けると、ここで ntpd クラスを次のように作成します。
<pre escaped="true">    class ntpd {
        package { "ntp":
            ensure =&gt; installed,
        }

        file { "/etc/ntp.conf":
            owner =&gt; root,
            group =&gt; root,
            mode =&gt; 0644,
            source =&gt; "puppet:///ntpd/ntp.conf",
            require =&gt; Package["ntp"]
        }

        @service { "ntpd":
            ensure =&gt; running,
            enable =&gt; true,
            hasrestart =&gt; true,
            hasstatus =&gt; true,
            require =&gt; [Package["ntp"], File["/etc/ntp.conf"]],
            subscribe =&gt; File["/etc/ntp.conf"]
        }
    }
</pre>
このコードでは、ntp デーモンのインストール、設定、および監視の間の関係が定められています。リソース タイプとして "package"、前例からの "file"、および "@service" (ここで "@" は仮想リソースを表す特殊構文ですが、今のところは無視してください) の 3 つが定義されているのがわかります。

先に述べたように、各リソースにタイプ、名前、および属性があります。これらのほとんどは自明ですが、関係を構築する属性は重要です。

この例の file リソースには "Package['ntp']" が必要であることがわかります。これは単に package リソースを指しています。@service リソースにも同じ要件が指定されていますが、さらにファイル タイプへの依存関係も追加されています。

"subscribe" 属性は、サービス タイプが、ファイル タイプに行われたすべての変更をリッスンして、必要に応じて再起動できるように指定します。"/etc/ntp.conf" に変更を加えると、サービスは次の Puppet 実行に際して自動的に再起動されます。

これらの関係を定義して、Puppet はバックグラウンドで依存関係グラフを作成します。この依存関係グラフでは、他のツールには備わっていない多くのユニークな機能が提供されます。
<h4>操作モードの不在</h4>
たとえば、この依存関係グラフでは、セットアップを "dry run" モードで '--noop' フラグを用いて実行できます。これによって、Puppet がシステムをどのように設定するかを正確にテストすることができます。これは、テスト用やステージング用のマシンを用いる場合でも、任意の本番インフラストラクチャに役立ちます。"noop" を使用すると、デプロイを行う前に新しいインフラストラクチャを迅速に開発できます。これは、Puppet の機能を他のツールと比較検討する際に見落としがちな機能です。
<h4>明示的なリソース依存関係</h4>
依存関係グラフを使用するもう 1 つの利点として、Puppet ではリソースの依存関係が常に明示的であることが挙げられます。アプリケーションの順序を心配せずに、リソースを自由に移動させることができます。上記の例で package リソースを別のモジュールに移動させても、ntpd のインストールと設定のプロセスに悪影響を与えることはありません。Puppet リソースは、それが依存する、または関心をもつと思われる他のリソースをリッスンして通知を行うことができます。リソース間の関係として順序が重要な場合には、これを明示的に指定する必要があります。Puppet はサーバーの状態を考慮した上で、設定の<a href="http://stochasticresonance.wordpress.com/2010/01/20/puppet-chef-dependencies-and-worldviews/">コンプライアンス</a>対応に努めます。

以上は Puppet のグラフベースの設計による利点のごく一部です。たとえば仮想<a href="http://projects.puppetlabs.com/projects/puppet/wiki/Virtual_Resources">リソース</a> (前例では service リソースが仮想リソースとして定義されています) などのオプションでは、類似のサーバー構造にまたがる関連リソースを扱う多くのオプションが利用できます。
<h3>Puppet の基本操作</h3>
Puppet はインフラストラクチャ内におけるクライアント/サーバー設定を念頭に置いて構築されていますが、利用を開始するのはとても簡単です。"puppet apply &lt;manifest&gt;" で任意の独立マニフェストを実行できます。上記の例で、ntpd 設定を "ntpd.pp" というファイルに配置する場合、"puppet apply ntpd.pp" だけを使用してそのサービスを管理できます。私の経験では、他のツールのスタンドアロン クライアントを利用するよりも、こちらの方がずっと優れています。この単一マニフェストから大きく本格的なインフラストラクチャ設定に移行するのも比較的簡単です。

次に示すのは NICS の<a href="http://www.slideshare.net/PuppetLabs/scalable-systems-management-with-puppet">プレゼンテーション</a>から引用したディレクトリ レイアウトの例です。これは高度な設定であり、あくまでこうした実装がどのようなものかを示す例に過ぎないことに留意してください。
<pre escaped="true">    /etc/puppet/
        auth.conf
        autosign.conf
        fileserver.conf
        puppet.conf
        tagmail.conf
        files/
            byhost/
                host1/
                host2/
                host3/
        manifests/
            nodes.pp
            site.pp
            classes/
                class1.pp
                class2.pp
        modules/
            module1/
                manifests/
                    init.pp
                files/
                templates/
</pre>
通常の場合、最初にモジュールの数を定義し、必要に応じてこれらをインポートします。Puppet ではサーバーが "ノード" として認識されます。 "ノード" は上の例の nodes.pp で通常は定義します。次にノード設定の例を示します。
<pre escaped="true">    node "webserver" {
        include ntpd
    }
</pre>
ここでは "webserver" というノードを定義して ntpd モジュールをインクルードしています。Puppet が "webserver" というホスト名のサーバー上で実行されるたびに、この ntpd モジュールが実行されます。現在のシステムに相違点がある場合、Puppet が状態をここで定義した設定に復元します。
<h3>まとめ</h3>
ここでは Puppet ならではの特徴をいくつか挙げ、比較的シンプルな例を使って Puppet の設計が一貫したインフラストラクチャの構築にいかに役立つかを示したつもりです。他のすべてのソフトウェアと同様 Puppet にも欠点はありますが、<a href="http://bitfieldconsulting.com/puppet-vs-chef">これについて</a> の<a href="http://bhuga.net/node/46">議論</a> は<a href="http://blog.loftninjas.org/2009/01/16/configuration-management-with-chef-announced/">他のサイト</a>を参照してください。

この記事だけでなく、今後も<a href="http://docs.puppetlabs.com/">ドキュメント</a>を参考にして知識を深めてください。また、Freenode IRC ネットワークの "#puppet" チャンネルや<a href="http://groups.google.com/group/puppet-users">メーリング リスト</a>からも役立つ情報を入手できます。
