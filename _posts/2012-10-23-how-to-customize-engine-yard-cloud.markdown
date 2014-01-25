---
layout: post
status: publish
published: true
title: Engine Yard Cloudのカスタマイズ
author: 安藤 祐介
author_login: yando
author_email: yando@engineyard.com
wordpress_id: 99
wordpress_url: http://www.engineyard.co.jp/blog/?p=99
date: 2012-10-23 10:48:32.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/EY3.Trdmrk.rgb_Hrzntl2.TM_.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/EY3.Trdmrk.rgb_Hrzntl2.TM_.png" alt="" title="EY3.Trdmrk.rgb_Hrzntl2.TM" width="302" height="165" class="alignnone size-full wp-image-45" /></a>

前回の記事ではEngine Yard Cloudの無料トライアルを利用してアプリケーションをデプロイする流れをご紹介しました。今回は実際にアプリケーションを構築してデプロイする場合に気になる各種カスタマイズの方法をご紹介します。

<h2>sshログイン後のsudo</h2>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/kabayaki91-—-deploy@domU-12-31-39-09-62-49_-—-ssh-—-82×25.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/kabayaki91-—-deploy@domU-12-31-39-09-62-49_-—-ssh-—-82×25.png" alt="" title="kabayaki91 — deploy@domU-12-31-39-09-62-49_~ — ssh — 82×25" width="579" height="349" class="alignnone size-full wp-image-113" /></a>
Engine Yard Cloudの稼働中のインスタンスにはsshでのリモート接続ができます。この際にはdeployユーザでログインしますが、ログイン後にsudoする事でroot権限での作業ができます。しかし直接加えた変更はインスタンスを停止した際に破棄されてしまうので、恒常的に必要になる設定を直接行うことは望ましくありません。調査目的や設定の検証などの用途であれば便利に利用できそうです。

<h2>crontabの設定はダッシュボードから</h2>
<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/Engine-Yard-Cloud-—-Scheduled-Jobs.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/Engine-Yard-Cloud-—-Scheduled-Jobs.png" alt="" title="Engine Yard Cloud — Scheduled Jobs" width="636" height="522" class="alignnone size-full wp-image-104" /></a>
コンソールでの作業が必要になる代表格がcrontabの設定です。幸いな事にcrontabの設定はダッシュボードからWeb上で行えます。簡易的な設定ではタスク名と実行するコマンド、実行頻度をフォームで指定します。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/Engine-Yard-Cloud-—-Scheduled-Jobs-1.png"><img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2012/10/Engine-Yard-Cloud-—-Scheduled-Jobs-1.png" alt="" title="Engine Yard Cloud — Scheduled Jobs-1" width="611" height="512" class="alignnone size-full wp-image-106" /></a>
詳細な設定画面では実際のcrontabの記述に近い形で自由に設定を記述します。特定の時間に実行させる必要があるようなタスクはこちらから設定します。

<h2>Chefのレシピで構成をカスタマイズ</h2>
環境に対して恒常的なカスタマイズを行う場合はChefのレシピが必要になります。レシピを記述しアップロードする事で環境の起動時や作成時の構築時に自動的に設定した内容が反映されるようになります。設定をChefで記述するのは最初は直感的ではないかもしれませんが、少ない記述量でシステムのさまざまな状態を設定できる優れたツールです。
レシピを利用したカスタマイズを行う場合は<a href="https://support.cloud.engineyard.com/entries/21009927-deploy-from-the-cli-engine-yard-cli-user-guide" target="_blank">Engine Yard CLI</a>をgemコマンドでインストールし、記述したレシピをアップロードします。

またレシピはgithubなどでも公開されており、多少の変更を加えるだけでさまざまな設定ができます。<a href="https://github.com/cookbooks/ey-timezone/blob/master/recipes/default.rb" target="_blank">下記のレシピ</a>ではサーバのタイムゾーンを任意の設定に変更し、タイムゾーンの影響を受ける幾つかのサービスを再起動している例です。

<pre>
timezone = "UTC"
service "vixie-cron"
service "sysklogd"
service "nginx"

link "/etc/localtime" do
  to "/usr/share/zoneinfo/#{timezone}"
  notifies :restart, resources(:service => ["vixie-cron", "sysklogd", "nginx"]), :delayed
  not_if "readlink /etc/localtime | grep -q '#{timezone}$'"
end
</pre>

実際のアプリケーションの運用環境を構築する場合は必要になるミドルウェアや設定が複雑になる場合があります。そういった構成を実現する為のカスタマイズの方法を覚えていくことはきっとみなさんのお役に立つでしょう。特にChefを活用したカスタマイズは応用の範囲が広いのでまた詳しくご紹介していければと思います。
