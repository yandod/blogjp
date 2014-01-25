---
layout: post
status: publish
published: true
title: Chef 11の最新情報
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 765
wordpress_url: http://www.engineyard.co.jp/blog/?p=765
date: 2013-04-02 10:01:52.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/What’s-New-in-Chef-11-—-Chef-Docs.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/What’s-New-in-Chef-11-—-Chef-Docs-300x192.png" alt="What’s New in Chef 11 — Chef Docs" width="300" height="192" class="alignnone size-medium wp-image-766" /></a>

最近、なにかと話題になる事の多いサーバの自動構築・管理ツールのChefですがちょうど現在バージョン10系から11系への転換期を迎えています。「いきなり11ってどういう事なの」という疑問を持った私の様な人の為にもChefのバージョンについて調べた内容を記事として公開します。

<h3>Chefの歴史</h3>
 Chefの最初のリリースは<a href="http://www.opscode.com/blog/2009/01/15/announcing-chef/" target="_blank">2009年1月15日、オープンソースとして最初のバージョン</a>は0.5.1としてApache Licenseでリリースされました。2009年1月15日というと、<a href="http://b.hatena.ne.jp/entry/jsmario.com.ar/" target="_blank">JavaScriptで実装されたスーパーマリオ</a>や<a href="http://jp.techcrunch.com/2009/01/15/20090114google-axes-dodgeball-jaiku-video-and-more/" target="_blank">GoogleがGoogle Notebooks、Google Catalogs、Dodgeball、Google Video、Google Mashup Editor、Jaikuなどのサービスの打ち切り</a>を決めた頃です。日本で大きく取り上げられるようになったのはつい最近ですが、かなり早いタイミングから現在知られているようなツールが公開されていた事になります。

<div class="note">Engine Yardの創業は2006年です。</div>

その後、順調にバージョンを刻んで0.9.18から0.10.0に到達します。(1.0ではなく)その後、<strong>0.10.10で0.x系のバージョンナンバーを最後に10.12.0として一気にChef 10と呼ばれるようになります。</strong>この10系は2011年6月から2013年2月にわたって長期間更新が続き広く知られるバージョンとなります。そして2013年2月に一部、アーキテクチャの変更を含む形で公開された最新の系統がChef 11という事になります。

<table style="width:60%">
<tr><th>バージョン</th><th>リリース日</th></tr>
<tr><td>0.5.1</td><td>2009/01/15</td></tr>
<tr><td>0.6.0</td><td>2009/04/28</td></tr>
<tr><td>0.7.0</td><td>2009/06/09</td></tr>
<tr><td>0.8.2</td><td>2010/02/28</td></tr>
<tr><td>0.9.0</td><td>2010/06/20</td></tr>
<tr><td>0.10.0</td><td>2011/05/02</td></tr>
<tr><td>10.12.0</td><td>2012/06/18</td></tr>
<tr><td>11.0.0</td><td>2013/02/04</td></tr>
</table>

<br class="clear"/>

<h3>Chef 11の最新情報</h3>
Chef 11ではサーバ側、クライアント側、クックブック内でのAPIについてさまざまな変更があります。小規模に利用していれば気が付かない部分ですが古い情報を参考にする場合に知っておくと良いでしょう。

<h4>Erchef - Chef 11からのサーバ</h4>
Chef ServerがErlangで書きなおされ、Erchefと呼ばれます。超巨大なOpscodeのHosted ChefやPrivate Chefの顧客のサポートから得た経験を元により高速でスケーラブルに書きなおされました。APIについてはオリジナルのRubyで実装されたサーバと互換性を保っています。またWeb UIについてもmerbからRails 3に移行されました。

公式のパッケージフォーマットはChef Clientで使われるOmnibusと同じになり、複数の環境で一貫した依存関係をすぐにインストールできるようになりました。全ての依存するライブラリはシステムとは分離され、 /opt にインストールされます。Omnibusに興味がある場合はこれらのパッケージの作成に使われているフレームワーク、<a href="https://github.com/opscode/omnibus-chef" target="_blank">omnibus-chefのリポジトリ</a>をご覧ください。

<h4>Knifeコマンドの強化</h4>
<a href="https://github.com/jkeiser/knife-essentials" target="_blank">knife-essentials</a>がマージされサーバとワークステーションの間でクックブックを管理するのに便利なサブコマンドが追加されました。

<pre>
knife diff
knife download
knife upload
knife list
knife show
knife delete
knife raw
</pre>

<h4>Chef Client</h4>
新機能の追加と既存の部分の重要なリファクタリングが行われました。これらの変更はchef-clientとchef-soloの双方でレシピやレシピの振る舞いに影響します。

<h5>Shefがchef-shellに</h5>
Shefがchef-shellにリネームされ、modeとattributeはredipe_modeとattributes_modeコマンドでセットするようになります。
<h5>ノードのAttirbuteの記述方法の変更</h5>
Attributeの予想外の挙動を防ぐ為、暗黙的な記述方法が廃止され、優先度(precedence)レベルを省略した記述はできなくなりました。

今後有効でなくなる記述例
<pre lang="ruby">
node[:my_attribute] = "value"
node.my_attribute_2 = "value"
</pre>

precedenceが指定されない場合はNormalであるとみなします。上記の例をChef 11移行に合わせると下記のようになります。

<pre lang="ruby">
node.normal[:my_attribute] = "value"
node.normal.my_attribute_2 = "value"
</pre>

<h5>attribute="value"の必須化</h5>

下記の記述は有効ではなくなります。
<pre lang="ruby">
node.default.my_attribute("value")
</pre>

上記の例を書き直すとこのようになります。
<pre lang="ruby">
node.default.my_attribute = "value"
</pre>

<h5>Knifeの出力の変更</h5>
以前のknifeは検索結果にIDというフィールドを追加していました。Chef 11からはKnifeは検索結果をノード名でグルーピングして表示します。古い出力は次のような形です。
<pre lang="cmd">
$ knife search roles:role_name -a ipaddress -fj
2 items found
{
  "results": 1,
  "rows": [
    {
      "ipaddress": "ec2-54-14-193-994.compute-9.amazonaws.com",
      "id": "i-a82555d2"
    }
    {
      "ipaddress": "ec2-994-79-96-9.compute-9.amazonaws.com",
      "id": "i-75555514"
    }
 ]
}
</pre>

新しい出力は下記のようになります。

<pre lang="cmd">
$ knife search roles:role_name -a ipaddress -fj
2 items found
{
  "results": 1,
  "rows": [
    {
      "i-a82555d2": {
        "ipaddress": "ec2-54-14-193-994.compute-9.amazonaws.com"
      }
    }
    {
      "i-75555514": {
        "ipaddress": "ec2-994-79-96-9.compute-9.amazonaws.com"
      }
    }
  ]
}
</pre>

<h4>RoleとEnviroment Attributeの変更</h4>
RoleとEnviromentのデフォルトはオーバーライドはattributesファイル内にあります。Chef11からはattributesにより複雑なロジックを取り込む為の変更が行われました。attributesファイルはシンプルにしておくべきなのは変わりませんが、プラットフォームのattributeを元にattributeを効率的に生成できるようになりました。

<h5>attributeからattributeを生成する</h5>
Chef 10以前では下記のコードはroleやenvironment内のsourceというattributeを変更するようには動作しませんでした。

<pre lang="ruby">
node.default[:app][:name] = "my_app"
node.default[:app][:env] = "development"

# Chef 10.xでは node.defaultを上書きするとこれらは誤った値になっていました。
# Chef 11ではroleのattributeとして正しく動作するようになりました。
node.default[:app][:database] ="#{node.app.name}_#{node.app.env}"
</pre>

Chef 10以前ではデフォルトとオーバーライドは単一のネストされたハッシュに保存されており。RoleとEnviromentのattributeはattributesファイルを評価した後に適用されていました。Chef 11以降ではroleとenviromentのattributeは別々に保存されており、run_listを展開してcookbookを実行する前に適用されるようになりました。

<h5>attributesをプラットフォーム毎にセットする</h5>
Chef 11ではChef::Nodeがplatform introspection mixin(プラットフォーム内省mix-in)をインクルードするようになり、下記のメソッドをattributesファイル内で利用できます。

<pre lang="ruby">
node.platform?(:platform1, :platform2)
node.value_for_platform()
node.platform_family?(:family1, :family2)
node.value_for_platform_family()
</pre>

<h5>挙動の変更</h5>
Chef 10ではレシピからdefaultやoverrideのattributeをセットでき、role enviroment attributeの全てを上書き出来ました。Chef 11からはnode.overrideには常にクックブックレベルのoverrideをセットします。クックブックレベルのattributeはEnviromentやRoleよりも優先度が低い為、<strong>レシピはroleやenvironmentでセットされた値を上書きしません。</strong>

<h4>その他</h4>
長くなってきたので残りについては簡単にまとめます。

<pre>
node.run_state Replaced
Subtractive Merge Removed
Chef::REST#run_request Removed
Delayed Notifications Changes
Single Notifies for Notification
Changes for Data Bag Encryption
Knife Configuration Parameter Changes
Remote File Mirror Support May Break Subclasses
The /clients endpoint returns JSON with a JSON class for edit (PUT) operations
The admin and validator flags are exclusive
Strict checking of top-level JSON keys
Creating an empty sandbox is now a 400 error
Error messages included in server error responses have changed
Some error codes have changes
knife reindex is not supported in Chef 11 Server
OpenId support has been removed
The Ruby server code has been removed
knife cookbook delete –purge is ignored by Chef 11 Server
</pre>

<h3>まとめ</h3>
かなりボリュームがありましたが、基本的には不具合に対処する為のリファクタリングの意味合いが強く、レシピ内で動的な処理をおこなっていなければ変更が行われた事にも気が付きにくいでしょう。特に各種attributeの評価順については既存の状態が意図に反しているという事で正しい状態に修正されたという風に考えて良いでしょう。


参考URL:
<a href="http://www.opscode.com/blog/2013/02/04/chef-11-released/" target="_blank">http://www.opscode.com/blog/2013/02/04/chef-11-released/</a>
<a href="http://docs.opscode.com/breaking_changes_chef_11.html" target="_blank">http://docs.opscode.com/breaking_changes_chef_11.html</a>
