---
layout: post
status: publish
published: true
title: 第3回 週末ランサーズにてCakePHP3についての講演をしました
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1829
wordpress_url: http://www.engineyard.co.jp/blog/?p=1829
date: 2013-11-12 15:10:49.000000000 +09:00
categories:
- Uncategorized
tags:
- 技術情報
- CakePHP
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/DSC06183.jpg"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/DSC06183.jpg" alt="DSC06183" width="1280" height="853" class="alignnone size-full wp-image-1830" /></a>

クラウドソーシングサービスのランサーズさん主催の勉強会、<a href="http://atnd.org/event/E0021059">第4弾　週末ランサーズ</a>にて、CakePHP3についての講演を行いました。まだ開発中のCakePHP3を実際に動かしてみたのは初めてでしたが、自分自身でも興味深い変化を見ることができました。

<script async class="speakerdeck-embed" data-id="3e8c10902d7501312a3002bd55941050" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

<h3>CakePHP3.0はPHP5.4以降とComposerが必須</h3>
PHP4対応を捨てたCakePHP2に引き続き、CakePHP3ではPHP5.3以前を廃止し、PHPの最新の構文を取り入れた形に大きく変わります。PSR-0/PSR-1に対応し<code>namespace</code>を使った形に全てのクラスが整理されています。また共通のメソッドの実装も基底クラスに持たせるのではなく<code>trait</code>に移行するなどの合理的な変更が加えられています。例えばControllerクラスの冒頭部分は下記のようになっています。

<pre lang="php">
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
</pre>


CakePHP2も現在ではPEARチャンネル経由でcomposerから利用できるようになっていますが、CakePHP3はさらにその対応が進みます。新規にCakePHP3のプロジェクトを作成するには下記のコマンドを実行するだけで必要な定義ファイルなどを指定したディレクトリに用意します。

<pre lang="cmd">
$ composer create-project -s "dev" cakephp/app /path/to/yourapp
</pre>

ComposerやPHP5.3移行の機能(namespace, trait, array short syntax)の利用は徐々に進んでいると思いますが、CakePHP3からはそれらの機能は当たり前のものとして使い、コードがより少なく抑えられる事になります。

<h3>新ORMはオブジェクトベース、クエリの遅延実行でパフォーマンス向上</h3>
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/20131109_cakephp3.032.png" alt="20131109_cakephp3.032" width="1024" height="768" class="alignnone size-full wp-image-1836" />

CakePHPの特徴でもあり弱点と言われていたのでModelが配列でデータを返すという点です。これによりViewで取り扱う全てのデータをControllerで配列として用意する事が多く、Controllerが肥大化しやすくなっていました。またViewまで処理が進むともはやデータには干渉できない事もあり、表示には実際は使わないデータまでJOINしているようなケースもあったかと思います。

<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/20131109_cakephp3.033.png" alt="20131109_cakephp3.033" width="1024" height="768" class="alignnone size-full wp-image-1837" />

CakePHP3では新しく<code>Cake/ORM</code>というクラス群が用意されオブジェクトベースのデータベース処理を提供します。従来のModelに近い構文でクエリを実行すると、Queryオブジェクトが作成され、これをViewへ渡します。
特筆すべき点はこの<strong>Queryオブジェクトから中身を取り出そうとするまではクエリは実行されません</strong>。よって条件の分岐などによってView内で結果を取り出されなかったクエリは実行されることはありません。これによりクエリの実行量を最適化しやすくなります。

サンプルアプリからの抜粋 (<a href="https://github.com/yandod/app" target="_blank">yandod/app</a>)
<pre lang="php">
<?php
namespace App\Controller;

use App\Controller\AppController;
use Cake\Database\ConnectionManager;
use Cake\ORM\Table;
use Cake\ORM\TableRegistry;

class SampleController extends AppController
{
    public $components = ['RequestHandler'];

    public function index()
    {
        $posts = new Table([
            'table' => 'posts',
            'connection' => ConnectionManager::get('default')
        ]);
        $results = $posts->find('all');
        $this->set('results', $results);
    }

    public function index3()
    {
        $posts = TableRegistry::get('post');
        //debug($posts);
        $results = $posts->find('all');
        $this->set('results', $results);
    }

}
</pre>

今後はこのORMクラスを使う形でModelクラスも書き換えられ、Modelにはバリデーションと適切なデータストアの呼び出しという役割が与えられ、純粋なORM部分が独立した形になると思われます。これによりModelはORMとは同一ではないという誤解されやすい点がコードとしてきちんと実装されることになります。

CakePHP3はまだまだ開発中でリリース時期もアナウンスされていません。まだ来年一杯くらいはCakePHP2が主流かと思いますが、今後のロードマップを把握しておくとCakePHP3がリリースされて以降の対応もしやすいのではないでしょうか。個人的にもCakePHP3への興味は上昇中です。今後も色々とチェックしていこうと思います。

<hr>
<h4>Engine YardはComposer標準対応。CakePHP2/CakePHP3が標準で動作</h4>
Engine Yard Cloudはサーバの構築や運用を自動化するだけではなく、アプリケーションの開発手法のベストプラクティスとして知られている機能もプラットフォームの機能に実装しています。PHPを利用したアプリケーションをデプロイする際は、Engine Yard上での稼働をご検討ください。無料トライアルでは500時間分、クラウド環境を利用してアプリケーションのテストを行えます。

<div style="text-align:center">
<p style="border: 1px solid black;width:468px;margin:auto"><a href="http://www.engineyard.co.jp/cloud_signup"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/04/468x60-banner.jpg" alt="468x60-banner" width="468" height="60" class="alignnone size-full wp-image-908" /></a></p>
</div>
