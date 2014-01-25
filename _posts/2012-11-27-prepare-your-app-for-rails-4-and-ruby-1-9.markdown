---
layout: post
status: publish
published: true
title: アプリケーションの Rails 4 / Ruby 1.9 対応準備(翻訳版)
author: anthonyaccomazzo
author_login: anthonyaccomazzo
author_email: aaccomazzo@engineyard.com
wordpress_id: 312
wordpress_url: http://www.engineyard.co.jp/blog/?p=312
date: 2012-11-27 05:48:04.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">
本記事は<a href="http://www.engineyard.com/blog/2012/prepare-your-app-for-rails-4-and-ruby-1-9/" target="_blank">英語版ブログで2012年2月21日に公開された記事</a>の翻訳版です。
</div>

<p>いつかこの日がやって来ることはわかっていました。</p>

<p>愛する Ruby 1.8.7 に別れを告げる日。Rails アプリケーションにまだ 1.8.7 を使用している方は覚悟を決めてください。Rails 4.0 の実行には Ruby 1.9 が必要です。</p>

<p>Rails マスター ブランチは 2 か月前に 4.0 に移行しました。これは、Rails 1.0 の発表から約 6 年後にあたり、その主な理由として挙げられたのは Rails の全ユーザーを Ruby 1.9 に移すということです。</p>

<p>Ruby 1.8 がなかった頃のことを思い出すのは難しいですね。言わば Rails は Ruby 1.8 と幼なじみの関係ですから。しかし、Rails コミュニティにも同じ高速リリースに歩調を合わせてもらうのは望ましいことといえます。</p>

<p>ご存知のように 1.9 には役に立つ機能が満載されています。パフォーマンスの向上だけでもアップグレードする価値は十分です。洗練された YARV インタープリターのおかげで Ruby は「のろま」の汚名を返上しました。ネイティブ スレッドおよびファイバーと併用して 1.9 を正しく使いこなせば、すべてのアプリケーションをぐんとスピードアップさせることが可能です。</p>

<p>さらに、Ruby 1.9 には最近話題の<a href="http://arstechnica.com/business/news/2011/12/huge-portions-of-web-vulnerable-to-hashing-denial-of-service-attack.ars" target="_blank">ハッシュによるサービス拒否攻撃</a>からの回復力があります。</p>

<p>思い切って移行する好機と納得いただけましたか。Ruby 1.8 と Ruby 1.9 の間では多くの変更点があります。以下に、コードを良好な状態に保つため、一般に調整が必要な部分を示します。</p>

<h3>ブロック ローカル変数</h3>

<h5>Ruby 1.8.7</h5>
<pre>
irb(main):001:0> x = 33
=> 33
irb(main):002:0> 3.times do |y|
irb(main):003:0>   x = 'chop' * y
irb(main):004:0>   puts x
irb(main):005:0> end

chop
chopchop
=> 3
irb(main):006:0> x
=> "chopchop"
</pre>

<h5>Ruby 1.9.1</h5>
<pre>
irb(main):001:0> x = 33
=> 33
irb(main):002:0> 3.times do |y;x|
irb(main):003:0>   x = 'chop' * y
irb(main):004:0>   puts x
irb(main):005:0> end

chop
chopchop
=> 3
irb(main):006:0> x
=> 33
</pre>

<h3>ハッシュが挿入順に配置される</h3>

<h5>Ruby 1.8.7</h5>
<pre>
irb(main):001:0> {:a => "a", :c => "c", :b => "b"}
=> {:a => "a", :b => "b", :c => "c"}
</pre>

<h5>Ruby 1.9.1</h5>
<pre>
irb(main):001:0> {:a => "a", :c => "c", :b => "b"}
=> {:a => "a", :c => "c", :b => "b"}
</pre>

<h5>または新しいハッシュ構文を使用した場合</h5>
<pre>
irb(main):002:0> {a: "a", c: "c", b: "b"}
=> {a: "a", c: "c", b: "b"}
</pre>

<h3>文字列はインデックス可能</h3>

<h5>Ruby 1.8.7</h5>
<pre>
irb(main):001:0> "lemon"[1]
=> "101"
</pre>

<h5>Ruby 1.9.1</h5>
<pre>
irb(main):001:0> "lemon"[1]
=> "e"
</pre>

<h3>{"a","b"} はサポートされない</h3>

<h5>Ruby 1.8.7</h5>
<pre>
irb(main):001:0> {"San Francisco", "California"}
=> {"San Francisco" => "California"}
</pre>

<h5>Ruby 1.9.1</h5>
<pre>
irb(main):001:0> {"San Francisco", "California"}
=> SyntaxError: (irb):1: syntax error, unexpected ',', expecting tASSOC
</pre>

<h3>Array.to_s はリテラルに解釈</h3>

<h5>Ruby 1.8.7</h5>
<pre>
irb(main):001:0> [2011, 2012].to_s
=> "20112012"
</pre>

<h5>Ruby 1.9.1</h5>
<pre>
irb(main):001:0> [2011, 2012].to_s
=> "[2011, 2012]"
irb(main):002:0> [2011, 2012].join
=> "20112012"
</pre>

<h3>多言語化</h3>

<h5>Ruby 1.8.7</h5>
<h6>文字列はバイトの集合</h6>
<pre>
irb(main):001:0> "해적선".size
=> 9
irb(main):002:0> "해적선".bytesize
=> 9
</pre>

<h5>Ruby 1.9.1</h5>
<h6>文字列はエンコードされた文字の集合</h6>
<pre>
irb(main):001:0> "해적선".size
=> 3
irb(main):002:0> "해적선".bytesize
=> 9
irb(main):003:0> "해적선".encoding.name
=> "UTF-8"
</pre>

<p>既存のコードを適切に修正することに加え、現在 <a href="http://beginrescueend.com/" target="_blank">RVM</a> を使用していない場合は、是非これをマシンで実行することを推奨します。RVM を使用すると Ruby の異なるバージョン間および異なる <a href="http://beginrescueend.com/gemsets/basics/" target="_blank">gemsets</a> 間を素早く切り替えることができ、移行に伴う困難をある程度軽減できます。Ruby のバージョンを素早く切り替えられれば、予期しないエラーの原因が特定しやすくなります。</p>

<p>最後に、これらの更新はすべて必ず別個のブランチで実行してください。問題が発生した場合にはコマンド 1 つで元に戻すことができます。</p>

<p>というわけで、新しいバージョンに是非移行しましょう。Rails 3 から Rails 4 への移行を Ruby のバージョン移行と同時に行うことだけは避けたいものです。今のうちに対処しておけば、きっと将来自分に感謝することになるはずです。</p>
