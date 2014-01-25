---
layout: post
status: publish
published: true
title: Rails 4 パート2：Rails 4の最新情報
author: J. Austin Hughey
author_login: austinhughey
author_email: austinhughey@engineyard.com
wordpress_id: 872
wordpress_url: http://www.engineyard.co.jp/blog/?p=872
date: 2013-06-26 13:29:20.000000000 +09:00
categories:
- Uncategorized
tags: []
comments:
- id: 48
  author: Rails 4 パート1：Rails 4の最新情報 (翻訳版) | Engine Yard Blog JP
  author_email: ''
  author_url: http://www.engineyard.co.jp/blog/2013/rails-4-changes/
  date: '2013-06-26 15:00:50 +0900'
  date_gmt: '2013-06-26 06:00:50 +0900'
  content: '[...] 注：これはRails 4の変更点と新しい特徴機能をお伝えする2部構成の投稿のパート1です。パート2は来週掲載されますので、そちらも併せてご覧ください。
    &gt;&gt; パート2公開いたしました。 [...]'
---
<div class="note">本記事は英語版のブログで<a href="https://blog.engineyard.com/2013/new-in-rails-4" target="_blank">2013年1月31日に公開された記事</a>の翻訳版です。</div>
注：これはRails 4の変更点と新しい特徴機能をお伝えする2部構成の投稿のパート2です。パート１をまだ読んでいない方は、<a href="http://www.engineyard.co.jp/blog/2013/rails-4-changes/">Rails 4 の変更点について説明したパート1</a>をご覧ください。

Rails 4には実用的で素晴らしい新機能も組み込まれています。私自身、これらの新機能にはとてもわくわくしていますし、みなさんもきっと同じ思いを抱くと思います。
<h3>Postgres H-Store</h3>
Rail 4のActiveRecordは、PostgreSQLの hstoreという拡張をサポートします。このデータベースの拡張によって、PostgreSQLの列（※カラムとも言います）に’hstore’という新しいデータ型が使えるようになります。hstoreは、文字列のみのハッシュを効率的に表示します。これは、事実上、テキスト列（カラム）のデータのシリアル化のようなものですが、これがネイティブのデータベースとなったおかげで、パフォーマンスが飛躍的に向上し、データベースに直接クエリを実行できるようになりました。つまり、みなさんはプラットフォームをMongoDB、CouchDB、Riakまたは他の似たようなスキーマレス データストアへとアップグレードしなくても、アプリケーションに利用できるスキーマレスなデータベースをわずかながら持つことができるようになったのです。

本格的なスキーマレス ソリューションではないものの、hsotreという拡張とそのRailsへの統合は、多くのアプリケーションにとって非常に好ましい変更となるでしょう。正規化されたある特定のモジュールのデータのほとんどを持っていても、いくつかの情報が「オンザフライ（その場で）」で定義されることを認めなくてはならない場合があります。このような場面で、hstoreは真価を発揮できます。

簡単な例を見てみましょう。みなさんのアプリケーションは、その場でオブジェクトの新しいキー／バリューのペアを定義する――ユーザーによって異なるオブジェクトのスキーマを定義する――ことができなくてはならないかもしれません。これは、例えばCMSの中の特定の種類のフォームかもしれません。医者は患者の情報をほしがりますが、イベント プランナーが欲しがる情報は全く違います。こうしたことは、今まではシリアライゼーションによって達成されたかもしれませんが、hstoreがあれば、これをネイティブなやり方で行い、クエリを実行することができるようになります。

<a href="https://github.com/softa/activerecord-postgres-hstore" target="_blank">activerecord-postgres-hstore</a> gemを使えば、すぐにPostgreSQLでhstoreを使い始めることができます。ライアン・ベイツの<a href="http://railscasts.com/episodes/345-hstore" target="_blank">Pro Railscast</a> は、その仕組みを説明し、いくつもの例でそれに対するクエリの実行方法をわかりやすく示しています。hstoreの拡張に関する詳細は、<a href="http://www.postgresql.org/docs/9.1/static/hstore.html" target="_blank">PostgreSQLの公式ドキュメンテーションをご覧ください</a>。環境データベースとしてPostgreSQL 9.1+を使うことによって、Engine Yardでhstoreを使えるようになったことは注目に値します。GitHubにある<a href="https://github.com/engineyard/ey-cloud-recipes/tree/master/cookbooks/postgresql9_extensions" target="_blank">postgresql9-extensions</a> カスタムChefレシピを見てみてください。ここにあるレシピで、hstoreだけでなく極めて多量の拡張を有効にすることもできますので、さまざまなオプションに目を通してみてください。
<h3>Array、MACADDR、INET、CIDR</h3>
PostgreSQLとRailsでサポートされる新しいデータ型について考える時、Rails 4のActiveRecordがPostgreSQL内部でArray, <a href="http://reefpoints.dockyard.com/ruby/2012/05/18/rails-4-sneak-peek-expanded-activerecord-support-for-postgresql-datatype.html" target="_blank">MACADDR, INET and CIDR</a>というデータ型をサポートすることは注目に値します。これらは通常はほとんどのデータベースで文字列型として格納されている一方で、PostgreSQLはそれぞれをサポートするネイティブのデータ型を提供しており、ActiveRecordはそれを利用することができます。

問い合せをされた時に、INETとCIDRデータ型は<a href="http://www.ruby-doc.org/stdlib-1.9.3/libdoc/ipaddr/rdoc/index.html" target="_blank">IPAddrクラス</a>のインスタンスに変換され、Arrayは当然ながらArray、MAC addressは文字列として出てきます。
<h3>ライブストリーミング</h3>
<a href="http://tenderlovemaking.com/2012/07/30/is-it-live.html" target="_blank">アーロン・パターソンは、Live Streaming（ライブストリーミング）というRail 4の新機能を発表しました</a>。この機能により、ブラウザの中でlong-pollingによってサーバから直接、エンドユーザーのブラウザに効率的にコンテンツをストリームさせることが可能になります。この処理においてブラウザが極めて重要な役割を果たしているということから、みなさんは直ちに明らかな大問題――インターネット エクスプローラーがまだそれに対応していない、という問題――に気づくはずです。この問題は、今後発表されるIEのバージョンで修正されるかもしれませんが、当分の間はライブストリーミングをマイクロソフトのブラウザで行うことはできません。

Rails 4のライブストリーミングは、みなさんのアプリケーションに大変興味深いたくさんの可能性を見せてくれます。最大の恩恵を受けるのは、リアルタイムデータに依存するアプリケーション――株式相場表示機と金融アプリケーション、ゲームなどでしょう。その他のアプリケーションも、ライブストリーミングの用途を見出すはずです。

Engine Yardでは、いくつかの理由からまだライブストリーミングをサポートしていません。まず第一に、弊社はウェブサーバーにUnicornとPassengerという二つのオプションがありますが、そのどちらもまだライブストリーミングをサポートしていません。<a href="http://blog.phusion.nl/2012/08/03/why-rails-4-live-streaming-is-a-big-deal/" target="_blank">Phusionが現在開発中のPassenger 4 Enterpriseは、Railsでライブストリーミングをサポートする予定</a>であり、Passenger 4がリリースされたら、それを弊社のスタックに統合しようと考えていますが、PhusionのEnterprise製品をどのように弊社のスタックに統合するか――または統合できるかどうか――はまだ模索中です。

このように書いたからといって、別にEngine Yardでライブストリーミングを使うことが不可能だと言っているわけではありません。ただ、この原稿を書いている時点では、すぐに使うことはできない、ということです。Engine Yardでは、アプリケーション サーバのオプションをもっとたくさん増やすことで、その状況を変えていこうとしています。例えば、Pumaは現在、Rubiniusと同じようにEarly Access機能として使うことができます。
<h3>キャッシュ ダイジェスト（別名：ロシア人形キャッシュ）</h3>
入れ子になったフラグメント キャッシュの中でバージョン番号を上げることにうんざりしている人にとって、これは願ってもない幸運です。Rails 4には、アプリケーションの中のすべてのフラグメント キャッシュ用にキャッシュ ダイジェストが組み込まれています。

例えば、投稿者（Authors）とポスト（Posts）をキャッシングするアプリケーションを持っているとしましょう。
<pre lang="ruby" escaped="true">
class Author &lt; ActiveRecord::Base
  has_many :posts
end

class Post &lt; ActiveRecord::Base
  belongs_to :author, touch: true
end
</pre>
（注：AuthorのPostが更新される時に、そのAuthorのupdated_atも強制的に変更されるようにするため、belong_toアソシエーションにtouch:trueを付けることは大変重要です）

たいていの場合、以下のようにフラグメント キャッシュするでしょう。
<pre lang="ruby" escaped="true">
<!-- app/views/authors/show.html.erb -->
&lt;% cache [‘v1’, @author] do %&gt;
<h1>&lt;%= @author.name %&gt;’s posts:</h1>
&lt;%= render @author.posts %&gt;
&lt;% end %&gt;

<!-- app/views/posts/_post.html.erb -->
&lt;% cache [‘v1’, post] do %&gt;
<div>&lt;%= link_to post.title, post %&gt;</div>
&lt;% end %&gt;
</pre>

問題は、フラグメント キャッシュを変更しようとするたびに配列の中のバージョン番号を上げなければならない、ということです。Rails 4のキャッシュ ダイジェスト機能を使えば、配列を省略して、RailsでMD5チェックサム キャッシュを自動的に生成することができます。ファイルを変更する時は、そのMD5チェックサムも変更されて、新しい「キャッシュ ダイジェスト」になります。

上記のフラグメント キャッシュは、キャッシュ ダイジェストを使って以下のようにはるかによいものにすることができます。
<pre lang="ruby" escaped="true"><!-- app/views/authors/show.html.erb -->
&lt;% cache @author do %&gt;
<h1>&lt;%= @author.name %&gt;’s posts:</h1>
&lt;%= render @author.posts %&gt;
&lt;% end %&gt;

<!-- app/views/posts/_post.html.erb -->
&lt;% cache post do %&gt;
<div>&lt;%= link_to post.title, post %&gt;</div>
&lt;% end %&gt;</pre>
ライアン・ベイツが<a href="http://railscasts.com/episodes/387-cache-digests" target="_blank">こちらのスクリーンキャスト</a>（無料）でもっと詳しく説明しています。みなさんも、今日からRails 3.2アプリケーションのこの機能を<a href="https://github.com/rails/cache_digests" target="_blank">cache_digests</a> gemと一緒に使い始めることができます。
<h1>セキュリティ関連</h1>
セキュリティに関して言えば、Railsは最新情報を常に把握しており、今回のリリースもその例外ではありません。しかし、最新のセキュリティ強化をうまく活用し、自分自身を守るためには――特に脆弱性が見つかり、パッチされ、公開されたあとは――自分のRails アプリケーションを最新の状態に維持しておくべきです。Engine Yardでは、現在利用できるものよりもいくつか前のマイナー ポイント リリースのアプリケーションを動作させているお客様をしばしば見受けます。例えば、2.3.15バージョンに上げれば既知のセキュリティの脆弱性から保護されるのに、なぜRails 2.3.2アプリケーションを動作させるのでしょうか？

これは小規模なPSAにすぎません。せめてマイナーポイントリリースを上げることによって、最新の依存性を保ちましょう。<a href="https://groups.google.com/forum/?fromgroups#!forum/rubyonrails-security" target="_blank">Rails Security mailing list</a>（投稿量は多くありません）を購読して、こうした問題に注意を払い、セキュリティ問題が公開されるたびにアプリケーションをアップグレードし、ステージング環境でデプロイメントをテストします。そうしなければ、脆弱性で知られるデータベースを使うことによって、インターネットをうろつきまわっているスクリプト キディーやボットの格好の標的になるだけです。
<h3>コントローラ内のMass Assignment Protection</h3>
私個人としては、RailsがとうとうRails 4でコントローラにmass assignment protectionを移したことを大変うれしく思っています。これは、コントローラ内部のオブジェクトの属性をホワイトリストまたはブラックリストに登録することによって行われます。簡単に例を見てみましょう。

仮に、レシピ（システム設定ではなく、食べ物のレシピ）を受け取るシンプルなウェブ アプリケーションをビルドしているとしましょう。レシピを作成する人は誰であれ、「シェフ」とし、そのレシピには名前、材料、作り方が含まれています。ここでは、便宜上、データ確認および承認の心配にはすでに対処されているものとします。
<pre lang="ruby" escaped="true">class RecipesController &lt; ApplicationController
  def create
    @recipe = Recipe.new(recipe_params)
    @recipe.chef = current_user # explicitly assign it to the right user
    if @recipe.valid? and @recipe.save
      redirect_to @recipe, 
                  :flash =&gt; { :notice =&gt; 
                  “Your recipe was added to the cookbook. Mmmm, tasty!” }
    else
      render :action =&gt; :new
    end
  end

private

  def recipe_params
    params.require(:recipe).permit(:name, :ingredients, :directions)
  end</pre>
このmass assignment protectionの新しい実行方法では、コントローラ内でprivateメソッドとして定義されているrecipe_params methodから返されるハッシュを受け取るように、Recipe.newに言います。このメソッドでは、基本的に”recipe”パラメータに関して許可されていないものはすべて取り除きます。ですから、このコントローラに以下を送ろうとすると（ハッシュによって表示）：
<pre lang="javascript" escaped="true">{name: "Texas Chili", ingredients: "hot stuff", chef_id: "123"}</pre>
“chef_id”パラメータは許可されていないため、recipe_paramsメソッド内で取り除かれます。その後、「サニタイズされた」ハッシュがRecipe.newに渡されます。こうすることによって、attackerが望む”chef”（author）にrecipeが勝手に割り当てられることを防ぐことができます。

これは、Railsの前のバージョンのmass assignmentのやり方とは大きく異なります。Rails 4では、これらの懸念事項をモデルの中に入れずに、コントローラの中に入れています。これは、多くの理由から、いささか議論の的となるかもしれません。

私は、<a href="http://www.refreshaustin.org/bash/" target="_blank">Austin Web Bash</a> で、オブジェクトの振る舞いの責任はどこにあるか、という議論について出席者のひとりと話したこと覚えています。純粋主義者の理論では、私たちはあらゆるインプットをオブジェクトに投入し、オブジェクト自体がそのインプットをどうすべきか知っていると信用できなければなりません。これが、Railsの前のバージョンでattr_accessible/attr_protectedを使って行われていたmass assignment protectionの仕組みです。みなさんは、あらゆるソース（テスト、HTTPを経由した本番データ、コンソール、アクセスなど）からあらゆるものを投入することができて、オブジェクトがそれを責任を持って管理していました。

しかし、この話には別の側面があります。Railsはウェブ アプリケーション フレームワークなのです。つまり、基本的に、みなさんにはユーザーと開発者という二つの入力ベクトルがあります。ユーザーのインプットは決して信頼されませんが、開発者のインプットは、まさに開発者というその本質によって、信頼されなければなりません。ユーザーにとって唯一の攻撃ベクトルはコントローラの中にあるため、モデルの内部よりもデータを保護するには道理にかなった場所のように見えます。これは、開発者にとって、さらに好都合です。なぜなら、開発者はプロジェクトのライフサイクルにわたって、データを徹底的に操作するのですから。プロジェクトの大半で、みなさんは最終的にデータを操作（場合によってはマイグレーションを通して）しなければコンソールにアクセスできない状況に遭遇します。いくつかの特定のプロパティに、必要性が生じるたびに手作業で‘object.method = “foo”’と打ちこむことは時間の浪費でしかなく、どうしようもなく退屈な繰り返しであり、生産性を落とします。モデル内にmass assignment protectionがあると、まさにそういう事態に直面することになります。プログラムに従ったマイグレーションまたはテストにおいてすら、たとえバックエンドで、信頼できるやり方でデータを操作していても、モデルレベルにmass assignment protectionがあることによって開発やテストで予期せぬ問題にぶつかる可能性があるのです。弊社は、これらの不安材料をコントローラに入れることにより、強力なユーザー インプット サニタイゼーションを維持しつつ、その問題をうまく防ぎます。

基本的に、これは選択の問題です。コントローラ ベースのインプットのみをサニタイズしてより柔軟な開発者データを運用するか、あるいは自分の望むオブジェクト設計を維持しながら柔軟性の低いデータ運用をするか、どちらを選択するかなのです。attr_protected/accessibleを使い続けたい方は、Rails 4アプリケーションのprotected_attributesジェムを使うことができます。

コントローラーレイヤーのプロテクションをすぐに使い始めたい方は、Rails 3.2.x.と互換性があるstrong_parametersジェムを見てみてください。
<h3>デフォルト ヘッダ</h3>
Rails 4には、あなたのアプリケーションから各レスポンスと一緒に返されるデフォルト ヘッダを指定することができるオプションが含まれています。相手方のブラウザがこれらのヘッダを適切にサポートしていれば、みなさんのアプリケーションを使う時のエンドユーザーの安全性を格段に高めることができます。

Rails 4では、各レスポンスに以下のヘッダがデフォルトで設定されます。
<pre lang="txt" escaped="true">config.action_dispatch.default_headers = {
'X-Frame-Options' =&gt; 'SAMEORIGIN',
'X-XSS-Protection' =&gt; '1; mode=block',
'X-Content-Type-Options' =&gt; 'nosniff'
}</pre>
ここに、他のヘッダを設定することも可能です。この特徴機能に関する詳細は、edge guide on securityをご覧ください。

この特徴機能は、モバイルおよびデスクトップ アプリケーション開発者にも有用です。この特徴機能を使って、すべてのリクエストにデフォルトでメタデータのいくつかのフォームを含め、それからそのメタデータを探すためのデスクトップ／モバイル アプリケーションをビルドすることもできるかもしれません。コントローラを通して各リクエストに常にヘッダをつけることができますし、このオプションによって各レスポンスに自動的にそれを行うこともできます。
<h3>暗号化されたクッキー</h3>
このpull requestは、暗号化されたクッキーがrails 4で機能する仕組みを説明しています。要するに、‘encrypted_cookie_store’という新しいsession_storeオプションが加わるのです。このセッション ストアは、クッキーが外へ出る時にそれを暗号化し、アプリケーションに読み込まれる時に解読します。これによって、エンドユーザーの不正を防ぎ、アプリケーションのセキュリティ レベルを上げます。

たとえこの特徴機能を使っても、クッキーに取扱いに慎重を要する詳細情報を格納することに対しては警告しなければなりません。これらのクッキーを暗号化／解読するのに使われるアルゴリズムはSHAベースのようです。つまり、GPUのクラスタといくつかのCUDAプログラミングにより、クッキー内の取り扱いに慎重を要するデータはもっと早く解読される可能性があるのです。なぜなら、SHAアルゴリズム ファミリーは、そう、bcryptほど計算コストが高くないからです。それだけでなく、クライアント サイドに取扱いに慎重を要する情報を格納ることは、一般的によい考えとは言えません。そのような情報は、ネットワーク層アクセスとみなさんのアプリケーションに保護された何らかのデータベースに格納されるべきです。

とにかく、クッキーを暗号化する機能は不正を避けるために非常に有用であり、Rails 4のクッキー／セッションの格納のデフォルトの方法となります。
<h1>Rails 4に搭載されていないものは？</h1>
非常に期待されていたにもかかわらず、どうやらRails 4.0には搭載されない機能がいくつかありました。そうした機能は、おそらく4.1で実現させるつもりでしょう。
<h3>バックグラウンド待ち行列</h3>
当初、Rails 4には、Sidekiqおよび／またはResqueが作業できるバックグラウンド待ち行列APIが組み込まれていました。しかし、今回のコミットでは、それらの機能をマスターから離して別々のブランチに移しました。これは、この特徴機能がいささか不十分であったことを示しています。ラファエル・フランカは、この特徴機能がRails 4リリースの障害であること、リリースを遅らせないようにこの機能の公開を延期したことに言及しています。
<h3>Asynchronous ActionMailer</h3>
バックグラウンド待ち行列APIの公開延期にともない、Asynchronous ActionMailerのサポートも延期されました。Asynchronous ActionMailerは、バックグラウンド待ち行列APIによって提供される機能に依存しているからです。
<h3>where.likeとwhere.not_like</h3>
モデルでの‘not_like’メソッド――例えばBook.where.not_like（title:”%Java%”）――を呼び出す機能を期待していた人は多いでしょう。しかし、今回のコミットはその特徴機能をActiveRecordからロールバックしています。DHH〈David Henemeier Hansson、デビッド・ハイネマイヤ・ハンソン：Railsを作った人〉は、なぜチームがそのコミットをロールバックすることに決めたのか、という4つの理由を記していますが、これにはみながみな同意しているわけではないようです。DHHは、その機能をActiveRecordの一部にせずに、コミュニティが自分たちのジェムにその機能を入れることを提案しています。反対意見の中でDHHは、 “greater_than_or_equal”（より優れているか、同じくらい）のようなものにDSLをさらに駆り立てる可能性が気に入らない、と言っています。パーセント記号の使用はRubyとの奇妙な構文の対立のように感じるし、また、そもそもLIKEクエリは極めて稀だ、とも言っています。
<h1>終わりに</h1>
Rails 4には、より安全で意味的に正しく、効率的なアプリケーションのビルドに役立つ、非常に興味深い新機能が多数搭載されています。Rails 4がリリースされ次第、コードベースをRail 4へアップグレード（ただし、規則正しく繰り返す方法で）することをお勧めします。

まだRails 2.xを使っている方には、少なくともRails 2.3.15（すべてのセキュリティ パッチがついた最新リリース版）でコードを安定させることをお勧めします。まず最初はひとつのスプリントを通して、それからもう一つ、または二つのスプリントを使ってRails 3.2に移行しましょう。リリースごとにマイグレートしてゆっくりと簡単に事を進めることもできますし、勇敢な方は3.2に真っ直ぐに進み、途中で問題が出現するたびに取り除いていくことも可能です。言うまでもなく、問題が大きくなる前にそれを探し出すために広範なテストを行うことが非常に重要になります。また、どんなものでも、性急に本番環境にデプロイする前に、ステージング環境にデプロイする（本番環境のクローンを作成して）ことを常にお勧めしています。

すでに3.2をご使用の方は、アップグレードが最も簡単でしょう。Rails 4の大半は、既存のソースコードをリファクタリングしたもので、それにいくつかの新しい特徴機能を取り入れただけだからです。暗号化されたクッキー ストアのメリットを活用し、mass assignment protectionをコントローラ レベルにリファクタリングする（みなさんがこの種のことに心から反対していて、その代わりに前述したジェムを使いたいのでない限り）ことを忘れないでください。

全体的に見て、Rails 4は、みなから愛されている有名なこのフレームワークに優れた改良を多数加えた素晴らしいリリースになることでしょう。とても楽しみにしていますし、みなさんも同じ気持ちだと思っています。

もっと詳しく知りたい方は、以下をご覧ください。
• <a href="http://blog.remarkablelabs.com/2012/11/rails-4-countdown-to-2013" target="_blank">http://blog.remarkablelabs.com/2012/11/rails-4-countdown-to-2013</a>
• <a href="http://blog.wyeworks.com/2012/11/13/rails-4-compilation-links/" target="_blank">http://blog.wyeworks.com/2012/11/13/rails-4-compilation-links/</a>
• <a href="http://weblog.rubyonrails.org/2012/11/21/the-people-behind-rails-4/" target="_blank">http://weblog.rubyonrails.org/2012/11/21/the-people-behind-rails-4/</a>
• <a href="http://edgeguides.rubyonrails.org/4_0_release_notes.html" target="_blank">http://edgeguides.rubyonrails.org/4_0_release_notes.html</a>
• <a href="http://rubyrogues.com/081-rr-rails-4-with-aaron-patterson/" target="_blank">http://rubyrogues.com/081-rr-rails-4-with-aaron-patterson</a>/
• <a href="http://vimeo.com/51181496" target="_blank">Rails 4 Whirlwind Tour: http://vimeo.com/51181496</a>
