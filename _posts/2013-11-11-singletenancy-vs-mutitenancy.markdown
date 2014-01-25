---
layout: post
status: publish
published: true
title: PaaSレイヤーの「シングルテナント」と「マルチテナント」はどちらが優位か？
author: 今中 崇泰
author_login: timanaka
author_email: timanaka@engineyard.com
wordpress_id: 1791
wordpress_url: http://www.engineyard.co.jp/blog/?p=1791
date: 2013-11-11 08:52:38.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
SaaSというクラウド事業モデルが出始めて以来、「マルチテナント」という言葉を耳にすることが多くなったのではないでしょうか。そして、今となってはあまり耳にしなくなっているかもしれません。しかし、誤解を解くために敢えてこの話題を取り上げたいと思います。

ではまず、「マルチテナント」という言葉の火付け役ともなった「SaaS」を含む、クラウドサービスの基本の3形態、そして「マルチテナント」とそれに相対する「シングルテナント」がどういったものなのかをおさらいします。
<h3>クラウドにおける基本の3形態</h3>
1999年に設立されたSalesforce.com社によって「SaaS」という言葉が生み出され、2006年に「クラウドコンピューティング」という言葉が普及して以降、クラウド上で提供されるソフトウェアを一般的に「SaaS」と呼ぶようになりました。そして、クラウドをはじめとする、あらゆるサービスの事業モデルを「XaaS」と名付ける流れが生まれました。

その「XaaS」と呼ばれるサービス事業モデルの中で、クラウドの最も基本的な事業モデルと位置づけられるものが3つあります。それは「IaaS (Infrastructure as a Service)」、「PaaS (Platform as a Service)」、「SaaS (Software as a Service)」という3形態です。これらは下図のように、システムの構成要素によって分類されています。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Cloud_Main_Types.png"><img class="alignnone size-large wp-image-1793" alt="Cloud_Main_Types" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Cloud_Main_Types-1024x517.png" width="1024" height="517" /></a>

これらの事業モデルの定義を簡単にまとめると以下のようになります。
<ul>
	<li><span style="line-height: 13px;"><strong>IaaS：</strong>サーバー、CPU、ストレージなどのインフラをサービスとして提供
</span></li>
	<li><strong>PaaS：</strong>アプリケーションを稼働させるためのプラットフォームをサービスとして提供</li>
	<li><strong>SaaS：</strong>アプリケーションをサービスとして提供</li>
</ul>
因みに、Engine Yardはこの3形態の中で「PaaS」に位置づけられるサービスを2006年から行っています。創業時はインフラも自社で構えてサービスを提供していましたが、2009年以降、IaaSを提供するベンダーと協業し、現在では、AWS、Windows Azure、Verizon Terremarkといった主要なベンダーの安定性のあるIaaSをインフラ層とするPaaSモデルになりました。
<h3>「シングルテナント」と「マルチテナント」</h3>
従来のASPに代わる事業モデルは、今や「SaaS」に取って代わりました。このパラダイムシフトこそが、「シングルテナント」と「マルチテナント」の議論を膨らませた一つの要因ではないかと思います。

というのも、「ASP」と「SaaS」を比較する際の項目として、「ASP」が「シングルテナント」であり、「SaaS」が「マルチテナント」であるという違いがあるからです。そしてまた、「SaaS」に欠かすことができない技術要素の一つが「マルチテナント」であるとすら言われています。
※ その他の「SaaS」の技術要素として、「マッシュアップ」などがあると言われています。

ではここで、「シングルテナント」と「マルチテナント」の違いを図に示したものを紹介します。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Single_vs_Multi.png"><img class="alignnone size-large wp-image-1792" alt="Single_vs_Multi" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Single_vs_Multi-1024x555.png" width="1024" height="555" /></a>

図で示された「シングルテナント」は、お客様ごとに専用サーバーなどの機材やデータベースを含む各種ソフトウェアなどを提供する事業モデルになります。そして一方、図で示された「マルチテナント」は、サーバーなどの機材やソフトウェアを複数のお客様で共有する事業モデルになります。

この図に示されていない考え方として、ハードウェアのみを共有し、その上で動作する仮想マシンをお客様ごとに提供することをインフラ層における「マルチテナント」と言います。まさにこれこそが「IaaS」という形態をさします。つまり、クラウドサービスの基本3形態の内、「SaaS」と「IaaS」が「マルチテナント」をベースにした事業モデルであると言えます。

このことから、『クラウドの世界は基本的に「マルチテナント」である』という見方が生まれているのではないでしょうか。

しかし、実のところ、クラウドサービスの基本形態の1つである「PaaS」においては「マルチテナント」だけでなく「シングルテナント」もあります。
<h3>「PaaS」における「シングルテナント」と「マルチテナント」とその比較</h3>
「PaaS」のインフラは仮想化されているため、インフラ層では「マルチテナント」であると言えます。しかし、プラットフォーム層については「シングルテナント」と「マルチテナント」の両方があります。それを図に示したものが以下になります。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Single_vs_Multi_for_PaaS.png"><img class="alignnone size-large wp-image-1794" alt="Single_vs_Multi_for_PaaS" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Single_vs_Multi_for_PaaS-1024x555.png" width="1024" height="555" /></a>

この図のとおり、「シングルテナント PaaS」も「マルチテナント PaaS」も、インフラリソースを複数のお客様のアプリケーションで共有している点では同じですが、プラットフォーム層を成すOS、ミドルウェア、ランタイムの扱いが大きく異なります。

「シングルテナント PaaS」は、お客様ごとに仮想マシンを提供するモデルです。つまりベンダーは、OSやミドルウェアやランタイムを実装した仮想マシンをそれぞれのお客様に提供し、お客様は自身の専用プラットフォームにアプリケーションをデプロイする仕組みです。

一方、「マルチテナント PaaS」は、大量の仮想マシン上に複数のお客様で共有利用するデータベースなどのミドルウェアを含むプラットフォームを形成し、それらをコンテナーという単位に分けてお客様に提供するモデルです。そしてお客様は、その割り当てられたコンテナーに自身のアプリケーションをデプロイする仕組みです。

では、「シングルテナント PaaS」と「マルチテナント PaaS」でどのような違いがあるのかを、5つの観点でまとめたものを以下にご紹介します。

<a href="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Single_vs_Multi_comptable.png"><img class="alignnone size-large wp-image-1795" alt="Single_vs_Multi_comptable" src="http://www.engineyard.co.jp/blog/wp-content/uploads/2013/11/Single_vs_Multi_comptable-1024x565.png" width="1024" height="565" /></a>

この結果からお察しのとおり、Engine Yardは「シングルテナント PaaS」を提供するベンダーです。われわれがEngine YardのPaaSを「商用グレードのPaaS」と謳い文句のようにあらゆる場でお伝えしているのは、上表のような優位性に富んだ「シングルテナント PaaS」を採用しており、そしてまた、その優位性を商用に発揮できる機能を備えているからです。

ではここで、上表の「安全性・安定性」と「メンテナンス性」という2つの観点をさらに掘り下げて違いを説明します。
<h4>「安全性・安定性」での比較</h4>
「マルチテナント PaaS」では上図の「共有のプラットフォーム コンポーネント」や「所有者管理レイヤー」といった層をPaaSがコントロールしています。まさにこの層こそが「マルチテナント PaaS」の中枢とも言える機能です。つまり、もしこれらの層がダウンするようなPaaSの障害が発生すると、あらゆるお客様のアプリケーションが一斉にサービス停止に陥ることを意味します。それに対して「シングルテナント PaaS」は、OSやミドルウェアやランタイムを実装した仮想マシンごと、個々のお客様に提供するモデルであるため、万一PaaSがダウンするなどの障害が発生したとしても、既に稼働しているアプリケーション環境は動作しつづける設計になっています。

また、Engine YardのPaaSに関して補足すると、東京を含む世界各国のAWSのリージョンを利用できるだけでなく、そのリージョン内の複数のアベイラビリティゾーンにEngine Yardが提供する仮想マシンを分散配置できるため、非常に高い安定性を備えています。
<h4>「メンテナンス性」での比較</h4>
プラットフォーム層のパッチをPaaSベンダー側が適用する「マルチテナント PaaS」の方が手間を省くことができて楽である、とお考えの方もいるかもしれません。しかし、もしご利用の「PaaS」にデプロイしているアプリケーションが、PaaSベンダーが強制的に適用するパッチによって支障を来したらどうでしょうか。もしそのアプリケーションが商用かもしくはアクセス数が非常に多いWebサービスだとしたら、Webサービスを運営するお客様の大きな損害に繋がりかねません。

やはり、いかなるセキュリティの脆弱性に対するパッチであったとしても、稼働中のアプリケーションの足回りであるプラットフォームに対して、PaaSベンダー側のスケジュールでパッチを適用することは危険極まりない行為である、というのがEngine Yardの見解です。

因みに、Engine Yardでパッチを適用する場合には、パッチ適用の事前検証用としてアプリケーション環境を複製するための「クローン機能」を用意しています。また、パッチ適用の作業自体はEngine Yardのダッシュボード画面から2つのボタンを順にクリックしていただくだけで完了できるなど、商用に向いたプロセスでありつつも、容易にパッチ適用作業が行える機能を備えています。
<h3>「シングルテナント PaaS」は「マルチテナント PaaS」と比べると割高？</h3>
「マルチテナント」というキーワードには、「コストが抑えられる」というキーワードがつきものです。では、「シングルテナント PaaS」は「マルチテナント PaaS」よりも割高ではないのか、という疑問も出てくるでしょう。

「シングルテナント PaaS」は柔軟にお客様の要求に応えられるよう設計されているため、「マルチテナント PaaS」よりも割高に感じられるかもしれません。しかし、今や何においても「自動化」が進んだ時代です。「シングルテナント PaaS」の内部には自動化の仕組みで埋め尽くされているため、PaaSベンダー側の運用コストも抑えられています。

したがって、決して「シングルテナント PaaS」は割高ではありません。

さらに続けると、「メンテナンス性」という点で「マルチテナント PaaS」では、パッチ適用やアップグレードのタイミングがPaaSを利用するお客様側で図ることができず、スケジュール上に載っていないタイミングでのアプリケーションのプログラム改修が発生するなど、逆に予期せぬコストでアプリケーションの保守コストが割高になっていることはないでしょうか。

事実として、「マルチテナント PaaS」からEngine Yardの「シングルテナント PaaS」に移行された多くのお客様から、『コスト削減につながった』という声をいただいています。
<h3>おまけ</h3>
Engine YardのPaaSは、ご紹介したとおりお客様のアプリケーション毎に仮想マシンをご提供するモデルです。

ただし、現行のEngine Yard Cloudの機能として、アプリケーションの開発言語やプラットフォームのコンポーネントが同一のものを採用している複数のアプリケーション群を、1つのプラットフォームにデプロイすることも可能です。つまり、他のお客様とは完全に切り離された「シングルテナント PaaS」でありながらも、お客様ご自身の複数アプリケーションでは1つのプラットフォームを共有するニーズにも応えられます。ある意味、お客様の中で閉じた「マルチテナント PaaS」に類似の利用方法もあります。

その他、参考情報としてEngine YardのPaaSの料金シュミレーターなど、いくつかWebページのリンクをご紹介します。
<ul>
	<li><a title="Engine Yard Cloudの利用料金シミュレーター(日本円ベース)" href="http://www.engineyard.co.jp/products/cloud/pricing" target="_blank">Engine Yard Cloudの利用料金シミュレーター(日本円ベース)</a></li>
	<li><a title="Engine Yard Cloudの利用料金シミュレーター(米ドルベース)" href="http://www.engineyard.com/products/cloud/pricing" target="_blank">Engine Yard Cloudの利用料金シミュレーター(米ドルベース)</a></li>
	<li><a title="Engine Yard Cloud / Managed テクノロジ スタック(stable-v2)" href="https://support.cloud.engineyard.com/entries/21009842?locale=67" target="_blank">Engine Yard Cloud / Managed テクノロジ スタック(stable-v2)</a></li>
	<li><a title="Engine Yard Cloud / Managed テクノロジ スタック(stable-v4)" href="https://support.cloud.engineyard.com/entries/23022773?locale=67" target="_blank">Engine Yard Cloud / Managed テクノロジ スタック(stable-v4)</a></li>
	<li><a title="お客様事例の紹介ページ" href="http://www.engineyard.co.jp/company/customers/case-studies" target="_blank">お客様事例の紹介ページ</a></li>
</ul>
&nbsp;

次回は、この記事の中で触れたEngine Yardの「クローン機能」についてご紹介したいと思います。
