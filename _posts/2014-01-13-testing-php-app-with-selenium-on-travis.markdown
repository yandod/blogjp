---
layout: post
status: publish
published: true
title: Travis CI上でPHPアプリのWebベースのテストを自動化する
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 2304
wordpress_url: http://www.engineyard.co.jp/blog/?p=2304
date: 2014-01-13 22:36:43.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2014/01/Travis_CI_-_Free_Hosted_Continuous_Integration_Platform_for_the_Open_Source_Community-2.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2014/01/Travis_CI_-_Free_Hosted_Continuous_Integration_Platform_for_the_Open_Source_Community-2-1024x509.png" alt="Travis_CI_-_Free_Hosted_Continuous_Integration_Platform_for_the_Open_Source_Community-2" width="1024" height="509" class="alignnone size-large wp-image-2305" /></a>

PHPなどのさまざまな言語のオープンソースプロジェクトのCI環境として利用されているTravis CIでWebベースのテストを実行してみました。
通常は純粋なコードベースのユニットテストを実行する事が多いかと思いますが、CMSやEコマースエンジンなどオープンソースで配布し、インストールして使うようなソフトウェアではWebブラウザベースでの機能テストを自動化したいというニーズがあるでしょう。Travis CIにはfirefoxがインストールされておりブラウザベースのテストが出来る事は知っていたのですが、今回年末年始の宿題的にテストを実行する為の設定をひと通り行ってみました。

説明を抜きにして動作が見たい方はGitHubとTravis CIへどうぞ

<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;">
<strong>yandod/candycane</strong>
<a href="https://github.com/yandod/candycane">https://github.com/yandod/candycane</a>
<strong>candycane on Travis CI</strong>
<a href="https://travis-ci.org/yandod/candycane">https://travis-ci.org/yandod/candycane</a>
</p>
<h3>テストの対象</h3>
今回はCakePHPに移植されたRedmine,CandyCaneのインストーラーを使ったインストールと管理画面へのログインをテストします。これにより機能の追加変更が初期のインストールプロセスを壊さないことを継続的に確認する事を目的としています。インストーラー及び管理画面へのログインには下記のような要素があります。

<ul>
<li>Webブラウザからインストール画面にアクセス</li>
<li><strong>AJAXを利用した実行環境の確認、次のステップへのリンクのクリック</strong></li>
<li>初期データベースの自動作成</li>
<li>管理者ユーザーでのログイン</li>
<li>管理者画面からの設定変更</li>
</ul>

今回は簡単なフローになっていますが、インストーラーと管理画面それぞれにJavaScriptを使った動的な画面制御が存在しています。この部分はブラウザでのテストを行わないと自動化できない部分でこれまで、自動化したテストができていませんでした。

<h3>ローカル環境でのテスト環境の構築</h3>
まずはローカル側でSeleniumとfirefoxを使ったテストの実行環境を構築する必要があります。検索したのですが残念ながら目的にあうChefのクックブックは見つからず、(中途半端なものは存在)今回はクックブックを作成しました。このクックブックをBerkshelfを経由してVagrantのVMに適用することでXvfbとfirefoxにSeleniumを使ったテスト環境が構築できます。またSeleniumの実行に必要なJavaは動けばいいのでこれもコミュニティクックブックをBerkshelfから突っ込んで適用します。クックブックの記述にあたっては下記のような試行錯誤がありましたが、皆様につきましては完成したクックブックを適用して頂ければ4メートル級の巨人の肩に乗れます。

<ul>
<li>PhantomJSのビルドにかかる様々な手間</li>
<li>SeleniumとFirefoxのバージョンの相性。</li>
<li>xvfbのセッションのサービス化</li>
<li>java -jarで起動したプロセスの再起動</li>
</ul>

<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;">
<strong>yandod/selenium-grid</strong>
<a href="https://github.com/yandod/selenium-grid">https://github.com/yandod/selenium-grid</a>
</p>

<strong>Vagrantfile</strong>

<pre lang="ruby">
Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  src_dir = './'
  doc_root = '/vagrant_data/app/webroot'
  app_name = 'candycane'
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.synced_folder src_dir, "/vagrant_data", :create => true, :owner=> 'vagrant', :group=>'www-data', :mount_options => ['dmode=775,fmode=775']
  config.berkshelf.enabled = true
  File.open('Berksfile', 'w').write <<-EOS
    cookbook 'apt'
    cookbook 'php5_ppa', '~> 0.1.1'
    cookbook 'omusubi', git: "https://github.com/yandod/omusubi.git"
    cookbook 'java'
    cookbook 'selenium-grid', git: "https://github.com/yandod/selenium-grid.git"
  EOS
  config.vm.provision :chef_solo do |chef|
    chef.add_recipe "apt"
    chef.add_recipe "php5_ppa::from_ondrej"
    chef.add_recipe "omusubi"
    chef.add_recipe "java"
    chef.add_recipe "selenium-grid"
  end
end
</pre>

<strong>余談：</strong>
自分しかやっているのを見たことがないですが、<code>Berksfile</code>をむりやり<code>Vagrantfile</code>に埋め込むやり方が管理が楽なので気に入っています。あくまで<code>Vagrantfile</code>だけでBerkshelfの恩恵を受けられます。


<strong>コミュニティクックブックについての衝撃的な知見</strong>

https://twitter.com/sawanoboly/status/418726580152573952

<h3>Seleniumのテストケースの記述</h3>
Seleniumを使ったテストケースについてはPHPUnitのサブパッケージであるPHPUnit_SeleniumをComposerで導入して記述しました。SeleniumIDEで生成したテストケースを使ってPhantomJSから実行する方法はテスト結果の出力があまり美しくありませんが、PHPUnit経由で実行すれば通常のPHPUnitのテスト結果と同様にCIに組み込むことができます。PHPUnit_Seleniumの利用方法については公式ドキュメントがあります。

<p style="background-color: #ffffcc; border: dotted black 1px; padding: 5px;">
<strong>PHPUnit Manual – 第17章 PHPUnit と Selenium</strong>
<a href="http://phpunit.de/manual/3.7/ja/selenium.html">http://phpunit.de/manual/3.7/ja/selenium.html</a>
</p>

実際にテストを記述してみて分かった間違いやすい点は下記の通りです。

<ul>
<li>PHPUnit_Extensions_SeleniumTestCase<br/>Selenium RCの古いAPIを使ったテストケース。スクリーンショットの取得やさまざまなアサーションが実装されている。</li>
<li>PHPUnit_Extensions_Selenium2TestCase<br/>Selenium WebDriverの新しいAPIを使ったテストケース。<strong><del datetime="2014-01-14T04:18:07+00:00">スクリーンショットの取得やアサーションなどは設計が変わった事で廃止されている。</del>フラグを立てるだけの方法から<a href="http://blog.a-way-out.net/blog/2014/01/14/phpunit-seleniumu2-screenshot-on-failure/" target="_blank">コールバックとリスナーを使った実装に変更</a>。</strong></li>
<li>適度なウェイトを設定しないとコード変更をしていなくてもテストが失敗する。</li>
<li>一定の条件を満たすまで待機する場合はコールバックを利用する。</li>
<li>URLは絶対パスで指定する</li>
</ul>

最大の落とし穴は<code>PHPUnit_Extensions_SeleniumTestCase</code>と<code>PHPUnit_Extensions_Selenium2TestCase</code>が全くの別物である点です。クラス名は1文字違いですが、共通するメソッドはほぼ無い別クラスです。Selenium RCがメンテナンスされていない現状からすると、基本的には<code>PHPUnit_Extensions_Selenium2TestCase</code>を利用するべきという事になります。

また所定のDOMなどが出現するまで動的に待機する場合にはコールバックを使った待機をしますが、ドキュメントにこの方法の記載がありません。<a href="https://github.com/sebastianbergmann/phpunit-selenium/blob/master/Tests/Selenium2TestCase/WaitUntilTest.php" target="_blank">PHPUnit自身のテストケース内</a>に実例があるのでこれを参考に実装しました。

<pre lang="php">
    public function testImplicitWaitIsRestoredAfterFailure()
    {
        $this->url('html/test_wait.html');
        $this->timeouts()->implicitWait(7000);

        try {
            $this->waitUntil(function($testCase) {
                $testCase->byId('testBox');
                return TRUE;
            });
            $this->fail('Should fail because of the element not exists there yet');
        } catch (PHPUnit_Extensions_Selenium2TestCase_WebDriverException $e) {}

        // in this case - element should be found, because of the implicitWait
        $element = $this->byId('testBox');
        $this->assertEquals('testBox', $element->attribute('id'));
    }
</pre>

実際にCandyCaneのインストーラーを実行するテストは下記のようになりました。インストーラーにアクセス後、ページのタイトルや次の画面へのリンクの表示を確認しながらステップを進めていく形です。また引用では省略していますが、最終的には管理者ユーザーでログインし、メール配信の設定を変更して保存するという管理者機能の挙動をテストしています。

<a href="https://github.com/yandod/candycane/blob/master/app/Test/Case/Selenium/InstallerTest.php">candycane/app/Test/Case/Selenium/InstallerTest.php at master · yandod/candycane</a>
<pre lang="php">
        $this->url('http://127.0.0.1/cc_install/cc_install/');

        $this->waitUntil(function($testCase){
            return $testCase->title();
        });

        $this->assertEquals('Installation: Welcome - CandyCane', $this->title());

        $this->timeouts()->implicitWait(3000);
        $this->waitUntil(function($testCase){
            $str = $testCase->byId('next-link')->text();
            return !empty($str);
         },100000);


        $link = $this->byId('next-link');
        $this->assertEquals('Click here to begin installation', $link->text());
        $this->moveto($link);
        $this->click();

        $this->assertEquals('Step 1: Database - CandyCane', $this->title());

        $this->select($this->byId('InstallDatasource'))->selectOptionByValue("mysql");
        $input = $this->byId('InstallDatabase');
        $input->clear();
        $input->value('test_candycane');
        $form = $this->byId('InstallDatabaseForm');
        $form->submit();
</pre>

<code>vagrant up</code>し、下記のコマンドを実行する事でテストが実行できるようになりました。

<pre lang="cmd">
cd /vagrant_data ;\
mysql -u root -e "drop database if exists test_candycane; \
create database test_candycane;";\
./vendor/bin/phpunit app/Test/Case/Selenium/InstallerTest.php
PHPUnit 3.7.28 by Sebastian Bergmann.

Configuration read from /vagrant_data/phpunit.xml.dist

.

Time: 9.12 seconds, Memory: 3.25Mb

OK (1 test, 9 assertions)
</pre>

<h3>Travis CI上でのテストの実行</h3>
最後にTravis CI上で同じようなテストを実行できるように<code>.travis.yml</code>を調整します。Travis CIのインスタンスにはfirefoxやXvfbなどは導入済みですので、Selenium Serverのダウンロード、Xvfbの起動などを before_scriptに設定します。

<pre lang="txt">
before_install:
  - "export DISPLAY=:99.0"
  - "sh -e /etc/init.d/xvfb start"
  - "wget http://selenium.googlecode.com/files/selenium-server-standalone-2.39.0.jar"
  - "java -jar selenium-server-standalone-2.39.0.jar > /tmp/selenium.log 2> /tmp/selenium.error &"
</pre>

また、Webからのアクセスを受けるにはApache2を経由してphp-fpmにアクセスする形になります。この際にvhostsの設定ファイルなどをリポジトリに含めておき、同じくスクリプトから設定します。

<pre lang="txt">
before_script:
  - sudo apt-get install apache2 libapache2-mod-fastcgi
  - sudo cp ~/.phpenv/versions/$(phpenv version-name)/etc/php-fpm.conf.default ~/.phpenv/versions/$(phpenv version-name)/etc/php-fpm.conf
  - sudo a2enmod rewrite actions fastcgi alias
  - echo "cgi.fix_pathinfo = 1" >> ~/.phpenv/versions/$(phpenv version-name)/etc/php.ini
  - ~/.phpenv/versions/$(phpenv version-name)/sbin/php-fpm
  - mkdir build
  - cp app/Test/travis/travis-ci-apache build/travis-ci-apache
  - sudo cp -f build/travis-ci-apache /etc/apache2/sites-available/default
  - sudo sed -e "s?%TRAVIS_BUILD_DIR%?$(pwd)?g" --in-place /etc/apache2/sites-available/default
  - sudo service apache2 restart
</pre>

これでVagrantのVMと同様の方法でテストが実行可能になりました。

今回の方法はやや泥臭い部分もありますが、PHPで動作するアプリケーションをSeleniumから自動でエンドツーエンドのテストを実行できる面白い方法です。オープンソースのプロダクトを公開している方はぜひテストの組み込みとTravis CIへのタスクの登録をしてみては如何でしょうか。コードを変更してもインストーラーや初期のログインなどの重要な機能が動作している事が担保されるというのはとても良いですよ。

<hr/>
<a href="http://ey.io/noyakshave"><img src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png"></a>
