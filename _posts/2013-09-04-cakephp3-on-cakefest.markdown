---
layout: post
status: publish
published: true
title: CakeFest2013で発表されたCakePHP3の未来
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1426
wordpress_url: http://www.engineyard.co.jp/blog/?p=1426
date: 2013-09-04 22:32:10.000000000 +09:00
categories:
- Uncategorized
tags:
- CakePHP
comments: []
---
<a href="http://www.flickr.com/photos/yandod/9650003293/in/set-72157635357819723"><img src="http://farm3.staticflickr.com/2836/9650003293_42cf3e3bc2_c.jpg" width="800" height="534" class="alignnone" /></a>

2013/8/29からの4日間、CakePHPの公式イベントであるCakeFestがサンフランシスコで開催されました。2年ぶりにアメリカでの開催となった今回は参加者も多くとても賑わっていました。今回のイベントの基調講演でCakePHP3の現状についていくつか情報が出てきましたのでご紹介します。<strong>なお今回のカンファレンスのノベリティがあるので、こちらの記事をはてブして頂いた方から抽選で3名の方に差し上げようと思います！</strong>

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/IMG_1718.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/09/IMG_1718-300x224.jpg" alt="IMG_1718" width="300" height="224" class="alignnone size-medium wp-image-1458" /></a>

<h3>CakePHP3の気になる新機能</h3>
<iframe src="http://www.slideshare.net/slideshow/embed_code/25796558" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen webkitallowfullscreen mozallowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/josezap1/cake-fest-2013-keynote" title="CakeFest 2013 keynote" target="_blank">CakeFest 2013 keynote</a> </strong> from <strong><a href="http://www.slideshare.net/josezap1" target="_blank">José Rodríguez</a></strong> </div>

<a href="https://github.com/cakephp/cakephp/tree/3.0" target="_blank">現在はブランチで開発されているCakePHP3</a>ですが、今年のうちにはベータなどのリリースが行われ最終的なリリースは来年になる見込みです。PHP5.3を飛び越えて5.4に対応する形になり名前空間などコードの見た目をぐっと現代的に変える変更が数多く行われています。今回の発表で言及された変更点は下記のとおりです。

<ul>
<li>PHP5.4以降に対応</li>
<li><strong>namespaceに完全対応</strong></li>
<li>DATABASE_CONFIGが廃止され、Configureに統合</li>
<li><strong>Composerに標準対応</strong></li>
<li>ルーティングの高速化(namedも。)</li>
<li>Adminルーティングのnamespace化</li>
<li>EventManagerの最適化</li>
<li>HttpSocketクラスの強化</li>
<li><strong>クエリビルダーの追加</strong></li>
<li>カスタムファインダーのチェーン化</li>
<li>Map Reduce</li>
<li>スキーママイグレーション</li>
</ul>

<h3>コードでみるCakePHP3</h3>
<img src="http://farm4.staticflickr.com/3798/9649992863_c5bd6e8b78_b.jpg" width="1024" height="683" class="alignnone" />

どこか昔ながらのPHPのコードの面影を残していたCakePHPですが、PHPの新機能を活用して現代的なコードになっています。たとえばコントローラーの基底クラスである<code>Controller</code>は下記のようになっています。

<pre lang="php">
<?php
namespace Cake\Controller;

use Cake\Core\App;
use Cake\Core\Configure;
use Cake\Core\Object;
use Cake\Core\Plugin;
use Cake\Error;
use Cake\Event\Event;
use Cake\Event\EventListener;
use Cake\Event\EventManager;
use Cake\Network\Request;
use Cake\Network\Response;
use Cake\Routing\RequestActionTrait;
use Cake\Routing\Router;
use Cake\Utility\ClassRegistry;
use Cake\Utility\Inflector;
use Cake\Utility\MergeVariablesTrait;
use Cake\Utility\ViewVarsTrait;
use Cake\View\View;

class Controller extends Object implements EventListener {

	use MergeVariablesTrait;
	use RequestActionTrait;
	use ViewVarsTrait;
}
</pre>

基底クラスではさまざまなコア機能にアクセスしているので名前空間の参照が多くなっていますが、アプリケーション側であれば必要な宣言のみを行うのでこれまでのコードとあまり変化はありません。

<pre lang="php">
<?php
namespace App\Controller;
class AppController extends \Cake\Controller\Controller {
}
</pre>

データベースの設定はさまざまな設定をまとめた<code>app/Config/app.php</code>に下記のように記述します。クラス宣言になっているので動的な制御がしづらかった点が通常のスクリプトになりました。Array Short Syntaxもつかわれていますね。

<pre lang="php">
$config = [
	'Datasources' => [
		'default' => [
			'className' => 'Cake\\Database\\Driver\\Mysql',
			'persistent' => 'false,',
			'host' => 'localhost',
			'login' => 'my_app',
			'password' => 'secret',
			'database' => 'my_app',
			'prefix' => false,
			'encoding' => 'utf8',
		],

		/**
		 * The test connection is used during the test suite.
		 */
		'test' => [
			'className' => 'Cake\\Database\\Driver\\Mysql',
			'persistent' => 'false,',
			'host' => 'localhost',
			'login' => 'my_app',
			'password' => 'secret',
			'database' => 'test_myapp',
			'prefix' => false,
			'encoding' => 'utf8',
		],
	]
];
</pre>

モデルについては配列地獄になっていた部分をオブジェクトに対応させる作業が進んでいます。従来のモデルとは別にORMクラスが整備されテーブルやレコードセットをオブジェクトとして扱えるようになりました。テストケースから抜き出したコードは下記のような形です。

<pre lang="php">
$this->connection = ConnectionManager::get('test');
$this->table = new Table(['table' => 'articles', 'connection' => $this->connection]);
$query = $this->table->find('all');
$results = $query->execute();
$expected = $results->toArray();
</pre>

DoctrineとCakePHPを合体させたようなコードになっていますが、規約ベースで設定せずに動作する点が大きな特徴です。クエリオブジェクトを使って検索条件を設定すると下記のようになります。

<pre lang="php">
$table = Table::build('article', ['table' => 'articles']);
Table::build('author', ['connection' => $this->connection]);
$table->belongsTo('author');

$query = new Query($this->connection, $table);
$results = $query->select()
	->contain('author')
	->order(['article.id' => 'asc'])
	->toArray();
</pre>

CakePHPのようなそうでないような不思議なコードになりました。とはいえ互換性には非常に気を使っているとのことですので従来のモデルの機能にプラスアルファされると思えばよいでしょう。機械的な書き換えについてはお馴染みのアップグレードシェルが用意されるそうですので、まずはCakePHP2のアプリケーションも移行できるかどうかを考える事になるでしょう。

<h3>VagrantとComposerについての発表</h3>
<script async class="speakerdeck-embed" data-id="4f495ff0f4900130a4091ec64b4e9d67" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

また昨年に引き続き講演が採択されたのでVagrantについての発表を行ってきました。日本語で以前行った内容を合体して英語にしたような形になっています。せっかくの機会ですので日本のコミュニティやCMSなどについて宣伝もしてみました。各国のCakePHPユーザもVagrantへの関心はとても高く、Vagrantに言及した講演が3本以上ありました。現在日本で流行っているVagrantが国際的にも大きなトレンドである事を発表者として確認できました。

<h3>コミュニティが力</h3>
<img src="http://farm6.staticflickr.com/5529/9650010343_2326e3bf1f_c.jpg" width="800" height="534" class="alignnone" />
CakePHPはコミュニティが発達しており、順調に成熟を続けているフレームワークです。今回のカンファレンスでもJames Wattsさんが基調講演でそういった主旨の事を発言しており、初級者、中級者のユーザーをどうやって大事にするかを第一に考えている事がよく見えました。この点については日本の皆さんに報告の生中継をしている時にもコメントをもらう事ができました。彼は今後のCakePHPを支える重要な人物だと思いますので、<strong>そのイカついスタイル</strong>も含めてぜひご覧ください。(16分ぐらいからが本編です、Jamesは48分ごろ登場)

<iframe width="853" height="480" src="//www.youtube.com/embed/Cn_0KBRZ5FA" frameborder="0" allowfullscreen></iframe>

<a href="http://www.flickr.com/photos/yandod/sets/72157635357819723/">CakeFest 2013 - a set on Flickr</a>
<a href="http://www.engineyard.co.jp/blog/2013/install-cakephp-on-composer/" title="CakePHPをComposerで導入する手順(Vagrantでのデモ環境同梱)">CakePHPをComposerで導入する手順(Vagrantでのデモ環境同梱)</a>
<a href="http://www.engineyard.co.jp/blog/2013/chef-and-vagrant-gives-you-next-dev/" title="Chef + VagrantによるPHP5.3 + MySQL + nginxの開発環境">Chef + VagrantによるPHP5.3 + MySQL + nginxの開発環境</a>
<a href="http://www.engineyard.co.jp/blog/2013/candycane-on-engineyard/" title="Engine Yard Cloud上のPHPにCandyCaneをデプロイ">Engine Yard Cloud上のPHPにCandyCaneをデプロイ</a>
<a href="http://eventifier.com/event/cakefest13/">CakeFest 2013 Photos #cakefest @cakephp | Eventifier</a>

<hr>
Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。PHPを利用したアプリケーションをデプロイする際は、Engine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>
