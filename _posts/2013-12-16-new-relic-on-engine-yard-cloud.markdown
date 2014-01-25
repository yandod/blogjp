---
layout: post
status: publish
published: true
title: New Relic on Engine Yard Cloud
author: 吉田 浩士
author_login: Hiroshi Yoshida
author_email: h-yoshida@esm.co.jp
wordpress_id: 2083
wordpress_url: http://www.engineyard.co.jp/blog/?p=2083
date: 2013-12-16 15:32:36.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<img src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/12/10586982624_6f0b906a6c_h-1024x682.jpg" alt="10586982624_6f0b906a6c_h" width="1024" height="682" class="alignnone size-large wp-image-2101" />
<div class="note">
<a href="http://www.esm.co.jp/index.html" target="_blank">株式会社 永和システムマネジメント</a>はEngine Yardのデベロップメント パートナーであり、さまざまな案件でEngine Yard Cloudをお使い頂いています。今回は実際にEngine Yard Cloudを使う際に必要になったNew Relicのカスタマイズの方法について、永和システムマネジメントの吉田 浩士様にゲストブロガーとして寄稿して頂きました。
</div>

私は<a href="http://www.engineyard.co.jp/products/cloud">Engine Yard Cloud</a>上で稼働しているRailsアプリケーション上でパフォーマンス監視のために<a href="http://newrelic.com/">New Relic</a>を使っています。
Engine Yard Cloudではアドオンとして様々な外部サービスを簡単に使用することができます。New Relicもその一つです。 本記事ではNew Relicを使う上での「メトリクスのカスタマイズ」と「デプロイの記録」という2つのTipsを紹介したいと思います。

<h2>メトリクスのカスタマイズ</h3>

New Relic は標準で以下のようにレスポンスにかかった時間の内訳を表示します。
それはController、View、Databaseといったメトリクスという単位で分かれています。

<p><img src="https://f.cloud.github.com/assets/1663465/1704945/7cd3adc4-60d4-11e3-86ee-8ae3bad67921.png" alt="default_result" /></p>

<p>標準の結果では不十分だった場合に、NewRelicではControllerやViewにまとめて計測されている結果をより細かくカスタマイズする手段を提供しています。</p>

<h3>Gem を使用する</h3>

いくつかのライブラリ向けにはすでに Gem が提供されていて、Gemfileに追加するだけで計測することができます。それがRedisだった場合、<a href="https://github.com/evanphx/newrelic-redis">newrelic-redis</a> を使うことで実現ができます。

<pre lang="ruby">
gem 'newrelic-redis'
</pre>

<p>実際にRedisとのやりとりにかかる時間を独立したメトリクスとして計測することができます。</p>

<p><img src="https://f.cloud.github.com/assets/1663465/1704944/7cd2b54a-60d4-11e3-8ff0-92a390ec8d1e.png" alt="use_gem" /></p>

<p>他にも <a href="https://github.com/stevebartholomew/newrelic_moped">Mongoid</a>, <a href="https://github.com/Viximo/newrelic-faraday">Faraday</a>用の Gem があります。詳しくは、<a href="https://github.com/newrelic/extends_newrelic_rpm">こちらのリポジトリ</a>を参照してください。</p>

<h3>自分で追加する</h3>

対応する Gem がないライブラリ、特定のメソッド等を計測したい場合、コードを書くことで実現できます。

例えば、コントローラ内で使っているメソッドを計測したい場合、以下のようなコードで実現することができます。

<pre lang="ruby">
require 'new_relic/agent/method_tracer'

class SampleController < ApplicationController
  include NewRelic::Agent::MethodTracer

  def index
    do_something
  end

  private

  def do_something
    # do somthing...
  end

  add_method_tracer :do_somethiing
end
</pre>


<code>newrelic_rpm</code> にはメトリクスを追加するためのモジュール<code>NewRelic::Agent::MethodTracer</code>が含まれています。
このモジュールに定義されている <code>add_method_tracer</code> メソッドに計測の対象にしたいメソッド名をシンボルで指定します。
これにより、指定したメソッド（この例では<code>do_something</code>）が独立したメトリクスとして表示されます。

<p><img src="https://f.cloud.github.com/assets/1663465/1731354/c073143a-6303-11e3-8063-8bba185a7a6f.png" alt="add_custom_metrics" /></p>

<h2>デプロイを記録する</h2>

New Relic にはデプロイがどの時間に行われたか記録する仕組みがあります。これを使うと、デプロイ前後でのパフォーマンスの変化を比較しやすくなります。

<p><img src="https://f.cloud.github.com/assets/1663465/1681471/696825aa-5d94-11e3-94a5-42c1b142f983.png" alt="image" /></p>

Engine Yard Cloudへのデプロイから、NewRelicへ自動でデプロイを記録するのは簡単です。
<code>newrelic_rpm</code>に含まれている<code>newrelic</code>コマンドとデプロイフックを組み合わせることで、自動でデプロイの記録ができます。

<ul>
<li>deploy/after_restart.rb</li>
</ul>


<pre lang="ruby">
require 'shellwords'
require 'yaml'

# Shell コマンドとして実行されるためエスケープをしている
def q(str)
  Shellwords.escape(str)
end

# アドオンの設定情報を読む
services = YAML.load_file("#{config.release_path}/config/ey_services_config_deploy.yml")
key      = services['NewRelic']['license_key']

# デプロイの説明を渡せるので、最新のコミットメッセージを使っている
message = `git log -1 --pretty='%s'`.chomp

run %(echo 'notify to newrelic...')
run %(cd #{config.release_path} && bundle exec newrelic deployments -a #{config.app} -u #{q config.deployed_by} -r #{config.revision} -l #{key} #{q message})
</pre>

<p>さらに、New Relic は Webhook をサポートしていて、デプロイが記録されたタイミングで <a href="https://www.hipchat.com/">HipChat</a>、<a href="https://campfirenow.com/">Campfire</a>、<a href="https://idobata.io/">Idobata</a> といった外部のサービスに通知することができます。（<a href="https://docs.newrelic.com/docs/alert-policies/alert-channels">参考</a>）</p>

<p><img src="https://f.cloud.github.com/assets/1663465/1692375/dbb6d60c-5e79-11e3-8d88-539119f65401.png" alt="selection_013" /></p>

<h3>まとめ</h3>

<p>本記事では私が実際に使っている2つのTipsを紹介いたしました。
New Relic は手軽にパフォーマンスを監視できますが、 少し手を加えることでより自分のアプリケーションに合った結果を見ることができます。
本記事で紹介した以外にも便利なAPIが用意されているので、興味があれば調べてみるといいかもしれません。</p>
