---
layout: post
status: publish
published: true
title: Nokogiri の基本(翻訳版)
author: aaronpatterson
author_login: aaronpatterson
author_email: yando+1@engineyard.com
wordpress_id: 227
wordpress_url: http://www.engineyard.co.jp/blog/?p=227
date: 2012-11-01 11:58:01.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">本記事は英語版ブログで<a href="http://www.engineyard.com/blog/2010/getting-started-with-nokogiri/">2010年1月14日に公開された記事</a>の翻訳版です。Engine Yard ブログでは少し趣向を変えて、コミュニティのメンバーによるゲスト投稿を募ることにしました。今回の (初めての!) ゲスト投稿は <a href="http://tenderlovemaking.com/">Aaron Patterson</a> 氏によるものです。Ruby コミュニティの長年のメンバーである同氏は Nokogiri の作成者でもあります。Seattle.rb の開発者とともにコーディングに勤しむ一方、世界各地で行われる業界の会議やイベントに出向いて Nokogiri や他の Ruby 関連のトピックについて講演を行っています。</div>
Nokogiri は XML ドキュメントと HTML ドキュメントを扱うためのライブラリです。Nokogiri は私の良き相棒 <a href="http://mike.daless.io/">Mike Dalessio</a> と一緒に開発しました。2 人とも Nokogiri を使って毎日 HTML や XML の作業を楽しんでいるので、読者の皆さんにもそれをお伝えしようと思ったわけです。この記事では以下のトピックについて説明します。
<ul>
	<li>Nokogiri のインストール</li>
	<li>基本的なドキュメント解析</li>
	<li>基本的なデータ抽出</li>
</ul>
この記事を通読されれば、きっと毎日の作業で Nokogiri を有効に利用できるようになると思います。
<h2>インストール</h2>
Nokogiri は、実際には Daniel Veillard 氏の優れた HTML/XML 解析ライブラリである <a href="http://xmlsoft.org/">libxml2</a> を包むラッパーです。Nokogiri はこの既存のライブラリをラップして活用するので、インストールには libxml2 のインストールが前提条件となります。幸い libxml2 は大半のシステムに移植済みなので、インストールはいたって簡単です。
<h3>OS X</h3>
OS X への libxml2 のインストールは <a href="http://macports.org">macports</a> から行うことを推奨します。OS X は libxml2 がインストールされた状態で出荷されますが、macports の方が新しいので、こちらを使用してください。

libxml2 を macports からインストールします。
<pre escaped="true">$ sudo port install libxml2 libxslt</pre>
次に nokogiri をインストールします。
<pre escaped="true">$ sudo gem install nokogiri</pre>
これで完了です。
<h3>Linux</h3>
Linux の場合も libxml2 をインストールする必要があります。libxml2 をインストールするコマンドは、使用しているパッケージ マネージャーと Linux ディストリビューションによって異なりますが、ここでは Fedora と Ubuntu の例を示します。

Fedora の場合:
<pre escaped="true">$ sudo yum install libxml2-devel libxslt-devel
$ gem install nokogiri</pre>
Ubuntu の場合:
<pre escaped="true">$ sudo apt-get install libxml2 libxml2-dev libxslt libxslt-dev
$ gem install nokogiri</pre>
<h3>Windows</h3>
libxml2 を Windows で扱うのは至難の業なので、<em>専用の</em> libxml2 を構築し、現在はこれを Nokogiri と同梱しています。Windows にインストールするには、<code>gem install nokogiri<span style="font-family: Georgia, 'Times New Roman', 'Bitstream Charter', Times, serif;">.</span></code> のコードを実行するだけで済みます。
<h3>しまった! 問題が発生!</h3>
Nokogiri には libxml2 のインストールを検索する基本的なインテリジェンスが備わっていますが、機転の利く開発者なら簡単にこれを回避できます。問題が発生した場合、まず libxml2 と libxslt 開発パッケージがインストールされていることを確認してください。すべてが正しくインストールされており、<em>それでも</em> Nokogiri がインストールできない場合は、<a href="http://groups.google.com/group/nokogiri-talk">Nokogiri メーリング リスト</a>に E メールをお送りください。できる限りお手伝いします。
<h2>基本解析</h2>
インストールが完了したら、実際に Nokogiri を使って作業をしてみましょう。Nokogiri は次のようないくつかの異なった戦略を用いて HTML や XML のドキュメントを解析します。
<ul>
	<li>DOM</li>
	<li>SAX</li>
	<li>Reader</li>
	<li>Pull</li>
</ul>
これらの戦略にはそれぞれ長所と短所があります。この投稿ですべての相違点を網羅することはできませんが、このうち一番よく使われる DOM インターフェイスは、一般に最も使いやすいとされています。したがって、ここでは DOM インターフェイスを中心に説明を進めます。

Nokogiri では HTML ドキュメントと XML ドキュメントのどちらを解析するかによって、主に 2 つのエントリ ポイントがあります。HTML ドキュメントの解析は次のように行います。
<pre lang="ruby" escaped="true">doc = Nokogiri::HTML(html_document)</pre>
XML ドキュメントの解析は次のように行います。
<pre lang="ruby" escaped="true">doc = Nokogiri::XML(xml_document)</pre>
これら関数は、いずれも IO オブジェクト<em>または</em>文字列オブジェクトを受け入れます。両者が IO オブジェクトを受け入れるので、次のように open-uri を直接 Nokogiri にフィードすることも可能です。
<pre lang="ruby" escaped="true">doc = Nokogiri::HTML(open("http://www.google.com/search?q=doughnuts"))</pre>
Nokogiri に IO オブジェクトをフィードすると、文字列を使用するより若干効率は上がりますが、自分にとって便利な方を選択してください。
<h3>データ構造</h3>
データ抽出の達人になるには、まず Nokogiri で返されるデータ構造を理解しなければなりません。特に、Nokogiri は HTML や XML のドキュメントをツリー データ構造に変換するという点を理解する必要があります。

たとえば、次のような HTML ドキュメントがあるとします。
<pre escaped="true">&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Hello!&lt;/title&gt;
  &lt;/head&gt;
  &lt;body id="uniq"&gt;
    &lt;h1&gt;Hello World!&lt;/h1&gt;
  &lt;/body&gt;
&lt;/html&gt;</pre>
これがメモリ内では次のようなツリーで表現されます。

<img src="//raw.github.com/tenderlove/article/master/html_tree.png" alt="HTML Tree" />

使用されるすべてのデータ抽出手法は、要するに、このメモリ内のツリーをスキャンする方法だということになります。このツリー構造を念頭に置いてデータ抽出に取り組めば、データ抽出完全制覇も夢ではありません。
<h2>データ抽出</h2>
HTML ドキュメントまたは XML ドキュメントをメモリ内のツリーに変換する方法については既に触れました。ここでは実際にこのツリーを使ってデータの抽出を行ってみます。まず、このツリーからデータを取り出すための戦略をいくつか見てみましょう。

メモリ内のツリーをスキャンするには 3 つの異なった方法あります。そのうち XPath と CSS は、ツリーのスキャン用に構築された小規模言語です。ここで検討する 3 つ目は、Nokogiri API によりツリーを手動でスキャンする方法です。
<h3>XPath の基本</h3>
<a href="http://www.w3.org/TR/xpath">XPath 言語</a>は XML ツリー構造を手軽にスキャンするために書かれていますが、HTML ツリーに使用することも可能です。次に Google 検索から結果のリンクを抽出するサンプル プログラムを示します。XPath を使用して目的のデータを検索し、続いて XPath の構文を分析します。
<pre lang="ruby" escaped="true">require 'open-uri'
require 'nokogiri'

doc = Nokogiri::HTML(open("http://www.google.com/search?q=doughnuts"))
doc.xpath('//h3/a').each do |node|
  puts node.text
end</pre>
このプログラムで使用される XPath は次のとおりです。
<pre escaped="true">//h3/a</pre>
この XPath を日本語に直すと次のような意味になります。
<blockquote>親タグの名前が "h3" であるすべての "a" タグを見つけなさい</blockquote>
したがって、このプログラムは親が "h3" であるすべての "a" タグを検索し、これをループ処理してテキスト内容をプリントします。

XPath は、冒頭の "/" がツリーのルートを表すディレクトリ構造のように機能します。スラッシュはタグの照合情報を区切る役目を果たします。スラッシュの間に何もない場合、これは "任意のタグに一致する" ことを示す、ある種のワイルドカードとして機能します。"h3" と "a" はタグ名のマッチャーで、タグ名が一致する場合のみマッチとなります。

これでタグ名を検索する方法はわかりましたが、先のプログラムを実行してみると、予想よりも多くの "a" タグが返されることがあります。そこでタグの何らかの属性 (ここでは "class" の値) に基づいて検索を絞り込む必要があります。XPath で属性値を照合するには、角かっこを使います。例をいくつか見てみましょう。

class 属性を持つ "h3" タグの照合は、次のように記述します。
<pre escaped="true">h3[@class]</pre>
class 属性が文字列 "r" に等しい "h3" タグの照合は、次のように記述します。
<pre escaped="true">h3[@class = "r"]</pre>
属性照合コンストラクトを使用して、上のクエリを次のように変更できます。
<pre escaped="true">//h3[@class = "r"]/a[@class = "l"]</pre>
この意味は次のとおりです。
<blockquote>class 属性が "l" に等しく、すぐ上の親タグ "h3" の class 属性が "r" である、すべての "a" タグを見つけなさい</blockquote>
元のプログラムをこの XPath で置き換えると、期待どおりの結果が得られます。

XPath クエリについての詳細は、<a href="http://www.w3schools.com/xpath/xpath_syntax.asp">w3schools のチュートリアル</a>および <a href="http://www.w3.org/TR/xpath">w3 の推奨事項</a>を参照するようお勧めします。

Nokogiri で XPath を使用する方法の詳細は、<a href="http://nokogiri.org/tutorials">Nokogiri チュートリアル</a>および <a href="http://nokogiri.org">RDoc</a> を参照してください。

次に、CSS の構文を見てみましょう。
<h3>CSS の基本</h3>
CSS は、ツリー データ構造を検索するための言語という点では XPath と似ています。このセクションでは XPath セクションと同じタスクを実行し、CSS の構文を分析していきます。

CSS では、タグ照合のパターンをスラッシュで<em>区切りません</em>。代わりに空白または "より大" 記号を使用します (実際には他にもありますが、ここではこの 2 つについて解説します)。では先の XPath を CSS として書き直し、構文を詳しく見てみましょう。
<pre escaped="true">//h3/a</pre>
これは、CSS では次のように記述されます。
<pre escaped="true">h3 &gt; a</pre>
文字 "&gt;" は、"a" タグが "h3" タグの直下の子でなければならいことを示します。ほとんどの CSS では、次のようにスペースが区切り文字とし使われています。
<pre escaped="true">h3 a</pre>
スペースの使用は、"h3" タグと "a" タグの間に任意数のタグが存在できることを示します。スペースは XPath の "//" に似ており、この CSS クエリを XPath で記述すると次のようになります。
<pre escaped="true">//h3//a</pre>
XPath と同様に、CSS でも角かっこを使って属性を照合できます。次に XPath から CSS への翻訳をもう 2 つ提示します。左辺が XPath で右辺が CSS です。
<pre escaped="true">h3[@class]        =&gt;  h3[class]
h3[@class = "r"]  =&gt;  h3[class = "r"]</pre>
このままの構文で機能しますが、CSS には "class" 属性を照合する省略形が備わっています。class 属性に "r" が含まれるすべての h3 タグを検索するには、次のように記述します。
<pre escaped="true">h3.r</pre>
上の 2 つの例には微妙な違いがあります。セレクター <code>h3[@class = "r"]</code> は<em>正確に一致</em>する必要があり、class の値が文字列 <code>r</code> と<em>完全に</em>等しくなければなりません。2 番目の例にあるセレクター <code>h3.r</code> は、「class 属性に r の値が含まれていなければならない」ことを意味します。したがって、次のタグと <code>h3.r</code> はマッチしますが、<code>h3[@class = "r"]</code> はマッチしません。
<pre escaped="true">&lt;h3 class="r foo"&gt;Hi!&lt;/h3&gt;</pre>
XPath セレクターとそれを翻訳した CSS セレクターはこのタグにマッチしませんが、"h3.r" セレクターはマッチします。ほとんどの場合、CSS の class セレクターは期待どおりに動作します。私が CSS セレクターで角かっこを使うのは、極めて具体的な条件が必要な場合に限られます。

以上を理解した上で、元のプログラムを CSS セレクターを使って次のように書き換えることができます。
<pre lang="ruby" escaped="true">doc = Nokogiri::HTML(open("http://www.google.com/search?q=doughnuts"))
doc.css('h3.r &gt; a.l').each do |node|
  puts node.text
end</pre>
CSS セレクターは XPath よりも簡潔で明確なクエリを作成できることが多いので、私のコードではふつう CSS クエリを使うようにしています。ただし、XPath で実行できても CSS では<em>不可能</em>なタスクもあるので、必要に応じて XPath クエリに立ち戻れるようにしておくと便利です。

次に、Nokogiri に備わっている基本的なノード API について見ていきましょう。
<h3>基本的なノード API</h3>
ツリー データ構造を扱うため、Nokogiri にはそのツリーをナビゲートするためのメソッドが用意されています。実際のところ、ここまで説明してきた XPath と CSS を使用するツリー スキャンは、すべて Ruby を使って手作業で実行することが可能です。ただ、手動のツリー スキャンは手間がかかり作業も細かいので、XPath や CSS といった言語の存在理由はそこにあるわけです。場合によっては、XPath または CSS に手動によるツリー スキャンを<em>加えた</em>組み合わせが一番簡単なこともあるので、この API を把握しておくことは重要です。

ドキュメント中のすべてのタグは Node というクラスによって表されます。ツリー内の各ノードに 0 個以上の子、 0 または 1 個の親、0 個以上の兄弟、そして 0 個以上の属性があります。Nokogiri には、任意の特定ノードにおけるこうした要素すべてにアクセスするためのメソッドが備わっています。たとえば次のように、任意の相対ノードにアクセスできます。
<pre escaped="true">node.parent           #=&gt; parent node
node.children         #=&gt; children nodes
node.next_sibling     #=&gt; next sibling node
node.previous_sibling #=&gt; previous sibling node</pre>
これらのノード アクセス メソッドを使ってツリーの手動スキャンを行えますが、私の場合、難しい部分は XPath や CSS クエリに任せて、必要な場合だけに手動のツリー アクセスを使用しています。

タグの属性にアクセスする場合、ノードは通常の Ruby ハッシュのように扱えます。たとえば、ノード上の属性を次のように取得し設定することができます。
<pre escaped="true">node['class']           #=&gt; the value of the class attribute
node['class'] = 'foo'</pre>
また、属性や属性値のリストを次のように取得することもできます。
<pre escaped="true">node.keys   #=&gt; list of attribute name
node.values #=&gt; list of attribute values</pre>
ノードを使って行える操作の詳細は、<a href="http://nokogiri.org/Nokogiri/XML/Node.html">ノード ドキュメント</a>および Nokogiri の<a href="http://nokogiri.org/tutorials">チュートリアル セクション</a>を参照してください。
<h2>まとめ</h2>
この記事は、HTML や XML の解析の達人を目指す皆さんの手助けとなることを願って執筆しました。ツリー データ構造を扱っていることを念頭に置き、XPath と CSS は HTML ドキュメントと XML ドキュメントの<em>両方</em>で実行できることを忘れないでください。

<a href="http://nokogiri.org/">当社のドキュメント</a>を是非ご参照ください。そして何か問題が発生した場合には、是非<a href="http://groups.google.com/group/nokogiri-talk">メーリング リストに参加</a>してください。
