---
layout: post
status: publish
published: true
title: Nginxの脆弱性(CVE-2013-4547)へのChefを使った対応
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 1893
wordpress_url: http://www.engineyard.co.jp/blog/?p=1893
date: 2013-11-22 11:35:42.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/nginx-announce__nginx_security_advisory__CVE-2013-4547_-2.png" alt="_nginx-announce__nginx_security_advisory__CVE-2013-4547_-2" width="1052" height="651" class="alignnone size-full wp-image-1894"style="border:1px solid black" />

<h3>脆弱性の内容</h3>

Nginxにセキュリティ設定を迂回できる脆弱性(CVE-2013-4547)が報告されました。この問題はNginxのバージョン、0.8.41 - 1.5.6が影響を受けると報告には記されています。内容については下記のようなセキュリティ設定を迂回できるというものです。

<pre lang="txt">
    location /protected/ {
        deny all;
    }
</pre>

迂回の方法はスペースを使ったURL,「/foo /../protected/file」やPHPなどの処理を呼び出す部分にやはりスペースがある事で実行できるとのことです。詳細については<a href="http://mailman.nginx.org/pipermail/nginx-announce/2013/000125.html" target="_blank">メーリングリストの投稿</a>を御覧ください。

<h3>Engine Yardでの対応</h3>

<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Engine_Yard_Cloud_—_Environment_ProductionJP_of_application_wordpress_jp.png" alt="Engine_Yard_Cloud_—_Environment_ProductionJP_of_application_wordpress_jp" width="1020" height="646" class="alignnone size-full wp-image-1896" style="border:1px solid black"/>

Engine Yardでは該当の問題に対する修正パッチを適用したクックブックを脆弱性の報告から<a href="https://support.cloud.engineyard.com/entries/28342587-Engine-Yard-Release-Updates-November-2013" target="_blank">2日後(2013/11/21)にリリース済み</a>です。
Engine Yardのダッシュボード上でアップデートを実施していない環境ではアップグレードボタンがハイライトされていますのでこちらをクリックします。

<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Engine_Yard_Cloud_—_Usage_Graphs.png" alt="Engine_Yard_Cloud_—_Usage_Graphs" width="1034" height="466" class="alignnone size-full wp-image-1897" style="border:1px solid black"/>

クックブックのアップグレードを行う事で適用される内容を確認の上で、アップグレードを実施できます。稼働中のアプリケーションへの影響の有無を事前に確認する必要がある場合は環境のクローンを数クリックで作成できますので、クローン上で適用を確認した上で適用する事をお奨めします。

Chefを使ったアプリケーション実行環境の構築は一般的になってきましたが、導入するミドルウェアのバージョンを明示的に運用できている例は必ずしも多くはないのではないでしょうか。例えば下記のような記述のクックブックでNginxを導入している場合、脆弱性の対応が確実に実施されていることをクックブックだけでは担保できません。
実行環境のプラットフォームのパッケージシステムで配布されているバージョンの確認や、現在導入されているバージョンの把握などを自力、またはChef Serverを使って行う必要があります。

<pre lang="ruby">
package "nginx"

directory node[:nginx][:dir] do
  owner 'root'
  group 'root'
  mode '0755'
end
</pre>

Engine Yardで提供しているクックブックは下記のような記述で導入されるソフトウェアのバージョンを事前に検証した組み合わせに固定した上で、定期的なバージョンアップを日々行っています。Engine YardではデフォルトではNginx1.2系を提供しておりパッチを適用したバージョンになっています。早期アクセス機能を使うことでSPDYを有効にした1.4.4も利用できます。
ただしこのような記述をする場合はパッケージの定常的な検証や実装する部隊、クックブックの配布方法などが必要になり、Engine Yardのサービスはそれをカバーしています。

<pre lang="ruby">
available_versions = {
    #  Used for nginx_unicorn, nginx_mongrel, nginx_nodejs, nginx_puma, nginx_fpm, nginx_thin
    "default" => {:version => '1.2.9-r5', :passenger_gem => "3.0.21"},
    "nginx_passenger4" => {:version => '1.4.4', :passenger_gem => "4.0.10"}
  }
</pre>

Engine Yardではこのような踏み込んだクックブックの運用やメンテナンスを行うことで開発者の方々が開発に集中できるDevOpsをサービスとして提供しています。Chefを使ってアプリケーションの実行環境を構築している方も運用の労力を削減する為にEngine Yardのご利用をご検討頂ければと思います。

<div><a href="http://ey.io/noyakshave"><img class="alignnone size-full wp-image-1889" style="border: 1px solid black;" alt="noyakshave_seminar_small" src="http://s3.amazonaws.com/engineyard.com/media_files/files/85/original/noyakshave_seminar_landscape.png" /></a></div>
