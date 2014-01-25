---
layout: post
status: publish
published: true
title: Rails 4 パート1：Rails 4の最新情報 (翻訳版)
author: J. Austin Hughey
author_login: austinhughey
author_email: austinhughey@engineyard.com
wordpress_id: 850
wordpress_url: http://www.engineyard.co.jp/blog/?p=850
date: 2013-06-14 09:00:38.000000000 +09:00
categories:
- Uncategorized
tags: []
comments:
- id: 47
  author: Rails 4 パート2：Rails 4の最新情報 | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/new-in-rails-4/
  date: '2013-06-26 13:29:23 +0900'
  date_gmt: '2013-06-26 04:29:23 +0900'
  content: '[...] 注：これはRails 4の変更点と新しい特徴機能をお伝えする2部構成の投稿のパート2です。パート１をまだ読んでいない方は、Rails
    4 の変更点について説明したパート1をご覧ください。 [...]'
---
<div class="note">この記事は英語版のブログで<a href="https://blog.engineyard.com/2013/rails-4-changes" target="_blank">2013年1月22日に公開された記事</a>の翻訳版です。記事中ではEngine Yard CloudはRails4をサポートしていないとありますが、現在はRails4をご利用頂けます。</div>

注：これはRails 4の変更点と新しい特徴機能をお伝えする2部構成の投稿のパート1です。パート2は来週掲載されますので、そちらも併せてご覧ください。
>> <a href="http://www.engineyard.co.jp/blog/2013/new-in-rails-4/">パート2公開いたしました</a>。

Ruby on Railsフレームワークの4つ目のメジャーバージョンの公開がいよいよ近づいてきました。公式なリリース日はまだ発表されていませんが、候補版は今年初めに公開される見通しです。今回のバージョンは、作成に1年以上を費し、内部の設計方法に大きく手を入れています。モジュラー化がさらに進み、主なコードベースの無駄をなくすために特徴機能の多くを別々のジェムに組み込んでおり、また、廃止予定の機能は公式にサポートされなくなっていますが、本当に必要な場合には使えるようになっています。

この原稿を書いている時点では、Engine YardのCloud製品はまだRails 4をサポートしていません。これは、みなさんがRails 4を試すことができない、ということではありません――みなさんがサポートできることは間違いありません。ただ、いくつかの特徴機能、特にライブ ストリーミングは、おそらく今すぐにはCloudで使えないことにご注意ください。Engine Yardはまだ製品にRails 4のサポートを組み込んでいないため、Rails 4アプリケーションのデプロイおよび動作にあたって遭遇する問題はすべて、バグではなく<a href="https://support.cloud.engineyard.com/forums/30086-feature-requests" target="_blank">機能リクエスト</a>として提出されなければなりません。言うまでもなく、Engine Yardのプラットフォームができる限り早くRails 4を完全サポートできるように努めてまいります。

<h1>Rails 4の大きな変更点</h1>

Rails 4には多くの変更およびリファクタリングが施され、新たにいくつかの機能が追加されています。この記事だけではそのすべてをカバーすることができませんが、特に興味深いものやインパクトの強いものを紹介します。

<h3>Ruby 1.9.3 以上が必須</h3>

すべての開発者が注意すべきRails 4の最も大きな変更点のひとつ――それは、この新しいフレームワークを実行するためにはRuby1.9.3以上が必要なことです。1.8.7のサポートは完全に打ち切られました。最近、弊社では1.9.3を使っているため、1.9.2のサポートについては気にする必要はありません。実際のところ、Jose Valim（ジョゼ・ヴァリム）による<a href="https://github.com/rails/rails/commit/4fa615a8661eb13d4bd8a7de4d839e9883ef26ec" target="_blank">このコミット</a>は、Rails 4にはRuby 1.9.3以上が必要であり、もしRUBY_Versionが1.9.3よりも前のものであれば、すぐに停止するようにはっきりとユーザーに伝えています。

これはみなさんにとって何を意味するのでしょう？　まず、1.8.7またはRuby Enterprise Edition（基本的に、1.8.7に性能調整機能がいくつかついたもの）を動作させている方は、とにかく今すぐにアップグレードを始めるべきです。1.8.7から1.9.3へのアップグレードがスムーズにできるかどうかは、アプリケーションやその依存性、それぞれのバージョンの間で廃止予定になっている可能性のあるもののうち何を使っているか（もし、あれば）によって、さまざまです。開発モードのインタープリターを1.9.3に変更して（<a href="https://rvm.io/" target="_blank">RVM</a>を使えば非常にシンプルです）、必ず十分なテストカバレッジでテストを行うようにしてください。普段とは違うアウトプットに注意し、1.9.3と互換性のない各アイテム用にお好きなトラッカー システムにストーリーを作成します。1.8 から1.9への移行についての詳細は、Engine Yardのアンソニー・アコマッゾ（Anthony Accomazzo）の<a href="https://blog.engineyard.com/2012/prepare-your-app-for-rails-4-and-ruby-1-9/" target="_blank">こちらの記事</a>をご覧ください。

とにかく、最新のパッチ レベルのコンポーネントを持つ、最新バージョンの安定したインタープリターで動作させることを強くお勧めします。理由はいくつかありますが、最も大きな理由はパフォーマンスとセキュリティの問題です。

<h3>"vendor/plugins" はもう必要ありません</h3>

Rails 4から、vendor/plugins ディレクトリはなくなりました。その代り、パスのあるBunderまたはGitの依存関係を使わなければなりません。

<h3>廃止予定の多くのアイテムが別個のジェムへ</h3>

Rails 4では廃止予定の機能がたくさんあり、それらは別個のジェムに移行されています。

<h3>ハッシュベースの動的なfinderメソッド</h3>

Railsの前回のバージョンでは、「古い」ActiveRecordクエリのシンタックスに対して常に警告が出されていたことを思い出す方もいるかもしれません。例えば、

<pre lang="ruby">
User.find(:first, :conditions => { … })
</pre>

Rail 4では、このシンタックスはもうサポートされません。この機能性をアプリケーションに戻すためには、activerecord-deprecated_finders gemをインストールする必要があります。
<a href="https://github.com/rails/activerecord-deprecated_finders" target="_blank">https://github.com/rails/activerecord-deprecated_finders</a>

<h3>ActiveRecord::SessionStore</h3>

データベースへのセッションの格納は興味深い特徴機能です。この機能には、いくつかの有用なアプリケーション――特に慎重を期する情報に対して――がありますが、ほとんどの場合、プレーンな古いクッキーを使うほどの性能性はありません。そのような理由から、ActiveRecord::SessionStoreはRails 4からなくなりました。この機能を呼び戻すには、activerecord-session_storeジェムを使う必要があります：
<a href="https://github.com/rails/activerecord-session_store" target="_blank">https://github.com/rails/activerecord-session_store</a>

さらに詳しく述べると、慎重を期する情報をクッキーに格納することは、いくつかの理由からよい考えとは言えません。暗号化されない（または、暗号化性能が弱い）ことはそうした理由のひとつに過ぎません。慎重を期する情報のもっとよい格納方法は、上記の情報をデータベース（ネットワーク層アクセスとアプリケーションに保護されているデータベース）に格納することです。そして、セッション オブジェクトのオブジェクトIDを参照するのです。ですから、セッションに完全なオブジェクトまたはオブジェクトに関するメタデータを設定する代わりにオブジェクトをデータベースに格納して、ユーザーのセッション内でそのIDを参照する（そして、それに関するメタデータは、例えばmemcachedかPostgreSQL hstoreに入れる）ことができます。

<h3>ActiveResource</h3>

ActiveResourceは、RESTベースのWebサービス用ORMです。ActiveResourceはRails 4から取り除かれ、搭載されません。<a href="https://twitter.com/guilleiguaran" target="_blank">ギレルモ・イグラン（Guillermo Iguaran）</a>がYeti Mediaブログで述べたところによると、<a href="http://yetimedia.tumblr.com/post/35233051627/activeresource-is-dead-long-live-activeresource" target="_blank">ActiveResourceが値するほど、コア チームがメンテナンスに熱心ではないから変更がされた</a>そうです。また、ActiveResourceが取り除かれたことで、ActiveResourcesの提供者――<a href="https://github.com/jeremy" target="_blank">ジェレミー・ケンパー（Jeremu Kemper）</a>率いる小さなチーム――が今までよりは注意を払うようになったそうです。取り除かれた後に新しい機能もいくつか追加されましたから、全体として見れば、ActiveResourceファンにとってポジティブな変更のように見受けられますし、この機能性が好きな人たちでその機能を得るために必ずしもRails全体を使う必要がない人たちにとっては非常に有用です。この機能をアプリケーションに取り込むには、’activesource’ジェムを組み込んでください：
<a href="https://github.com/rails/activeresource" target="_blank">https://github.com/rails/activeresource</a>

<h3>Rails Observers、Page、Action Caching</h3>

Rails 4では、”Rossian Doll（ロシア人形）”キャッシング ストラテジーを支持して、PageとAction caching（キャッシング：データをキャッシュメモリに保存すること）は廃止される予定です。DHH（ David Heinemeier Hansson）は、キャッシングの仕組みを説明するジェムをGitHubに用意しています。：詳しくは、<a href="https://github.com/rails/cache_digests" target="_blank">https://github.com/rails/cache_digests</a>をご覧ください。

とにかく、pageとaction cachingがなくなった今、ActiveRecord Observesの必要性はほとんどなくなってしまいました。多くの場合、これらのobserversは、Rails 4の新しいキャッシング スキームのおかげで必要なくなったキャッシュの無効化に使われます。キャッシュの無効化以外では、コールバックの方がよいオプションであるにもかかわらず、永続化オペレーションのごみ廃棄場として誤用されがちです。そこで、Rails 4は、observers、Pageまたはaction cachingなしでリリースされます。

これらをアプリケーションに呼び戻すには、以下をご覧下さい。

<ul>
<li><a href="https://github.com/rails/actionpack-action_caching" target="_blank">https://github.com/rails/actionpack-action_caching</a></li>
<li><a href="https://github.com/rails/actionpack-page_caching" target="_blank">https://github.com/rails/actionpack-page_caching</a></li>
<li><a href="https://github.com/rails/rails-observers" target="_blank">https://github.com/rails/rails-observers</a></li>
</ul>

<h3>memcache-clientに代わるDalli</h3>

memcachedには、memcache-clientではなくDalliが使われるようになりました。Dalliはmemcache-clientよりもかなり速く、スレッドセーフ――これはコミュニティでますます懸念されているトピックです――であるため、多くの開発者にとってこの変更は歓迎すべきことでしょう。Dalliを使うためには、まだ追加されていなければGemfileに”dalli”ジェムを追加し、mem_cache_storeにキャッシュ ストアを設定します。

<h3>新しいデフォルトのテストロケーション</h3>

RailsとTDDの初心者は、しばしばデフォルト設定とテスト ロケーションのネーミングに混乱します。例えば、"Models"はユニットテスト、"controllers"は"ファンクショナルテストに該当することなどです。Rails 4では、こうしたことがかなりわかりやすくなります。デフォルトのテスト ロケーションは、rspecのRailsテスト用のネーミングに少し近くなりました。

<pre>
app/models -> test/models (was test/units)
app/helpers -> test/helpers (was test/units/helpers)
app/controllers -> test/controllers (was test/functional)
app/mailers -> test/mailers (was test/functional)
</pre>

テストのネーミングとその目的についての興味深い議論を読みたくなったら、この<a href="https://github.com/rails/rails/pull/7878" target="_blank">プルリクエストに関する議論</a>を見てください。当初、インテグレーションテスト（test/integration）は受け入れテストに改名される予定でした。残りのプルリクエストは歓迎されましたが、この変更だけは、何が受け入れテストで、何がそうでないのか、という会話が盛り上がりました。最終的には、コミッターである<a href="https://github.com/blowmage" target="_blank">blowmage</a>はacceptanceのコミットを捨てて、integrationはそのままにしておくことを決定し、Railsの複数のコア チーム メンバーがこの決定に賛成したのです。

<h3>PATCH Verb</h3>

Railsは、かなり長期間にわたって、既存のリソースの修正に”PUT” HTTPメソッドを使ってきました。しかし、HTTP仕様書は、意味的にPUTをリソースの完全な説明と見なしています。言い換えれば、意味的に言って、PUTはアップデートされるオブジェクト全体の完全な説明を含んでいなければならないのです。それゆえに、私たちはしばらくの間、PUTを経由してRESTfulアップデートを行う時に、変更する必要のあるオブジェクトの断片を送ることしかしておらず、実際はいささか「間違った」ことをしてきたわけです。

Rais 4が、この機能でパッチ verbを代わりに使うように変更したのはこのためです。そして、文字通り、PATCHはサーバ上のオブジェクトに関する完全な説明ではなく、データの新たな断片のみを送るようになっています。これは、<a href="http://tools.ietf.org/html/rfc5789" target="_blank">RFC 5789</a>に述べられているように、HTTPセマンティックスにもっと一致しています。

RailsのすべてのRESTfulフォームと同様に、使用されるメソッドが”PUT”ではなく”PATCH”だと定義する秘密の”_method”フィールドが生成されます。そして予想通り、ルーティングはコントローラ内の「アップデート」アクションにPATCHメソッドを割り振ります。

下位互換性を保つ策として、前のPUTメソッドもRails 4.0で「アップデート」をルーティングしつづけます。ですから、例えば、既存のAPIはアップグレード後も通常通り機能しつづけるはずです。

PATCHメソッドについては、Railsのブログでさらに詳しく説明されています。これは全般的に素晴らしい変更であり、下位互換性のある方式で行われているため、開発者のアップグレード パスは確実にスムーズなものになるでしょう。

<h3>デフォルト設定でスレッドセーフ</h3>

Ruby開発者は、しばらく前からGILフリーの本当の意味でのマルチスレッディングを求めてきました。そして、Railsのコントリビューターたちは、MRIだけが本番でアプリケーションを動作させる方法ではないことを知っています。マルチスレッデッドのサーバとアプリケーションは、メモリのセグメントを共有し、コードの並列実行を可能にすることによってパフォーマンスを大幅に向上させる効果があります。
しかし、”MRI”として知られているRubyの標準インタープリターは、本当の意味でのマルティスレッドではありません。例えば、MRIはひとつのスレッドがI/Oで待っている時にコードを並行に実行したり、下層のCライブラリに並行に実行をさせることができますが、実際のRubyコードは、グローバル インタープリター ロック（GIL）があるために、今も同期で実行されています。

Railsにはしばらく前からスレッドセーフにコードを動作させるオプションがありますが、それをデフォルトでできるようにはしていませんでした。Rails 4からは、それが可能になります。設定オプションを修正してスレッドセーフ サーバを再起動させるだけでほとんどのRailsアプリケーションでこれを今すぐ実現できることを考えれば、この変更は一部の人たちが期待しているほど大きなものではありませんが、Railsコミュニティが並行のWebアプリケーション コードを動作させる必要性にますます適合してきているという事実に注目させます。

スレッドセーフ設定については、アーロン・パターソンがこちらでもっと詳しく説明しています！：
<a href="http://tenderlovemaking.com/2012/06/18/removing-config-threadsafe.html" target="_blank">http://tenderlovemaking.com/2012/06/18/removing-config-threadsafe.html</a>

パート1はこれで終わりです。来週掲載されるパート2では、Rails 4の新しい特徴機能について説明します！
