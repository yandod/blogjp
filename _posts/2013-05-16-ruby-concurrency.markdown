---
layout: post
status: publish
published: true
title: Rubyの並行処理で学んだこと――パート１(翻訳版)
author: Jeremy Budnack
author_login: jeremybudnuck
author_email: jeremybudnuck@engineyard.com
wordpress_id: 830
wordpress_url: http://www.engineyard.co.jp/blog/?p=830
date: 2013-05-16 10:00:57.000000000 +09:00
categories:
- Uncategorized
tags: []
comments: []
---
<div class="note">この記事は英語版のブログで<a href="https://blog.engineyard.com/2013/ruby-concurrency" target="_blank">2013年2月5日に公開された記事</a>の翻訳版です。</div>

Engine Yard のPaaS製品は非常に複雑である上に、数千ものサーバーに及んでいます。弊社のアプリケーションを素早く確実に動作させるには、並行処理と並列処理をよく理解する必要があります。私は、自らの開発努力でこの問題を解決しようと、並行処理という困難な世界を探求しました。この投稿はその要約です。後編となるパート2では、並列処理に重点を置いて説明する予定です。

<h3>ハードウェア？</h3>

この問題をハードウェアで解決しようとすることはできます。しかし、CPUがネックなのであれば、コアごとのスピードをある程度まで上げることはできても、最終的には役に立たなくなってしまいます。サーバーの数を増やすにしても、同じことが言えます。次々とシリアル処理を行っても、追加されたサーバーごとの処理装置の数は決まっているからです。

<h3>「シリアル処理」のシリアル・キラーになろう！</h3>

最近問われているのは、コアスピードよりもコアの密度です。CPUは、処理速度が高速化しているのではありません――コアの数が増えているのです。しかし、みなさんがアプリケーションを非常に小さな塊に分けて、そのすべてが同時に動作（つまり「並列処理」）できるようにしない限り、このマルチコアのメリットを活用することはできません。

<h3>並行処理vs.並列処理</h3>

このように複雑な問題に取り組むときは、並行処理と並列処理の違いを知ることが重要です。並行処理とは、さまざまな時間帯にまたがるタスクを進行させるプログラムの能力です。この能力のおかげで、複数の「スレッド」を同時に動作させることができます。ひとつのスレッドがI/O上でスリープまたは待機している時は別のスレッドが優先的に動作し始めるため、CPUの時間を最適利用することができます。並行処理について考える時は、「スレッド」を思い浮かべましょう。

並列処理は、複数のタスクを同時に実行する能力のことです。並行処理を並列処理のことだと勘違いする人もいますが、並行処理は同じCPUのリソースを得るためにスレッド同士が互いを尊重しあっているわけですから、並列処理ではありません。例えば、MRIには、Global Interpreter Lock（グローバル インタプリタ ロック：GIL）というものがあります。みなさんのコードが複数のスレッドを使っていても、それらのスレッドはGILによって一度にひとつずつ動作しているのです。ですから、みなさんのアプリケーションは「本当の意味では」マルチスレッドではないのです！ そうする代わりに、MRIは動作しているスレッドを素早く切り替えて、各スレッドに短い処理時間を提供しているのです。みなさんのI/Oは並列処理で動作しているかもしれませんが、Ruby コードは一度に一つのスレッドしか動作していません。

幸いなことに、みなさんにはいくつかの選択肢があります！　私が推奨するのはRubiniusです。Rubiniusとは、Rubyプログラミング言語のためにゼロから実装される動的な言語プラットフォームです。バイコード インタプリタ、近代的なガベージ コレクタ、マシンコードへのJITコンパイラ、グローバルインタプリタロックのないネイティブスレッドが組み込まれているため、ハードウェアがサポートすれば複数のルビー スレッドが並行して動作します。Rubiniumは、エヴァン・フォニックスによって考案され、Engine YardのDirkjan Bussinkと ブライアン・フォードがメンテナンスを行っています。

この議論で最も重要なことは、RubiniusにはGILがないため、本当の意味でマルチスレッディングをサポートしている、ということです。Rubiniusでは、それぞれのスレッドがネイティブのオペレーティング システムの軽量プロセス（light weight process：LWP）に割り振られています。Rubiniusは、上記の弊社プロジェクトで使用しているルビー インタプリタです。

スレッディングを正しく実装したとしても、他のオプション――アプリケーションへのマルチプロセスやマルチマシン機能の追加など――に目を向けなければ、みなさんが使えるハードウェアのメリットを完全に享受しているとは言えません。これらの技術については、パート2で説明します。

Rubyの並行処理（Ruby concurrency）と並列処理に関するさらに徹底した議論については、エヴァン・フォニックスの投稿をご覧ください。

<h3>スレッディング</h3>

スレッドを作成する時、スレッド ブロック内のコードは、スレッドを生成するメイン アプリケーションと並行して動作します。

弊社の実例用アプリケーションを使って、シンプルな通貨ダウンローダーから始めてみましょう。

<pre lang="ruby">
require 'net/http'
 
# Our sample set of currencies
currencies = ['ARS','AUD','CAD','CNY','DEM','EUR','GBP','HKD','ILS','INR','USD','XAG','XAU']
 
currencies.each do |currency|
    puts Net::HTTP.get("download.finance.yahoo.com","/d/quotes.csv?e=.csv&f=sl1d1t1&s=USD#{currency}=X")
end
puts "DONE!"
</pre>

このままで十分機能しますが、次の通貨をそれぞれ一度に一つずつ処理しているため、少し時間がかかります。これを、並行処理（並列処理）を使ってもっと速くしてみましょう。並行処理を進めると、以下のようになります。

<pre lang="ruby">
require 'net/http'
 
# Our sample set of currencies
currencies = ['ARS','AUD','CAD','CNY','DEM','EUR','GBP','HKD','ILS','INR','USD','XAG','XAU']
# Create an array to keep track of threads
threads = []
 
currencies.each do |currency|
    # Keep track of the child processes as you spawn them
    threads << Thread.new do
        puts Net::HTTP.get("download.finance.yahoo.com","/d/quotes.csv?e=.csv&f=sl1d1t1&s=USD#{currency}=X")
    end
end
# Join on the child processes to allow them to finish
threads.each do |thread|
    thread.join
end
puts "DONE!"
</pre>

生成させたスレッドを追跡するために、配列を使っていることがわかります。私たちは、たいていの場合、スレッドを手に負えない状態にするよりも、すべてのスレッドが終了（または「結合」）するまで待ってから次に進みたいと思います。それに、親スレッドを子スレッドに結合（待機）させなければ、子スレッドは動作終了前に死んでしまう可能性があります。ループ結合がなければ、アウトプットは以下のようになります。

<pre lang="cmd">
DONE!
</pre>

ループ結合があれば、アウトプットは以下のようになります。

<pre lang="cmd">
"\"USDCAD=X\",0.9967,\"11/5/2012\",\"4:23pm\"\r\n"
"\"USDINR=X\",54.575,\"11/5/2012\",\"4:23pm\"\r\n"
"\"USDAUD=X\",0.9649,\"11/5/2012\",\"4:23pm\"\r\n"
"\"USDILS=X\",3.9054,\"11/5/2012\",\"4:23pm\"\r\n"
"\"USDCNY=X\",6.2443,\"11/5/2012\",\"4:23pm\"\r\n"
"\"USDEUR=X\",0.7818,\"11/5/2012\",\"4:23pm\"\r\n"
"\"USDXAG=X\",0.0321,\"11/5/2012\",\"3:31pm\"\r\n"
"\"USDGBP=X\",0.6259,\"11/5/2012\",\"4:23pm\"\r\n"
"\"USDHKD=X\",7.7501,\"11/5/2012\",\"4:23pm\"\r\n"
"\"USDARS=X\",4.773,\"11/5/2012\",\"4:23pm\"\r\n"
"\"USDUSD=X\",0.00,\"N/A\",\"N/A\"\r\n"
"\"USDXAU=X\",0.0006,\"11/5/2012\",\"4:20pm\"\r\n"
"\"USDDEM=X\",0.00,\"N/A\",\"N/A\"\r\n"
DONE!
</pre>

<h3>スレッドがめちゃめちゃになってしまった！</h3>

よくできました――これで、スレッドの使い方がわかりましたね。しかし、まだ問題は残っています。この例で、仮に500を超える通貨を使えるようアプリケーションを拡張するとしましょう（実際に500も通貨があるとして、の話ですが）。これは、私がアプリケーション全体を使って500もの同時スレッドに呼び出しを入力して動作させるということでしょうか？　もちろんそれは可能ですが、みなさんが100のコアCPUを持っていない限り、あまりよい考えとは言えません。以下でその理由を述べましょう。

どんなマルチスレッド環境でも、コンテキストスイッチ（context switching）が発生します。コンテキストスイッチは、他のスレッドがCPUサイクルを使えるように、あるスレッドを止めてそのスレッドの状態とコンテキストを保存するプロセスのことです。競合するスレッドが同様のやり方で中断されると、オリジナルのスレッドのコンテキストと状態が読み込まれ、オリジナルスレッドが優先権を得れば動作します。

他にもう一つ注意点があります――実際のコンテキストスイッチの行為そのものはCPUサイクルを使います。単純に可能な限りスレッドを増やした場合、システムが実際にデータを処理する時間よりも、コンテキストスイッチを行う時間のほうが多くなってしまう可能性があります。そうするとアプリケーションが遅くなります。

では、スレッドを適切にスケジュールするにはどうしたらよいでしょうか？　私がよく使っているのは、 producer-consumer モデルです。このモデルには、2つのメインスレッドがあります。Producerスレッドがやるべき作業を提供し、Consumerスレッドがそれらの作業ユニットを読み込んでその作業を行うスレッドを起動させます。

これを実行するためには、いくつかのコミュニケーション方法が必要です。

・Producerは、Consumerに作業ユニットを提供する方法が必要です。
・Consumerは、他のスレッドをスケジュールできるように、どのスレッドが作業しているか、どのスレッドが作業終了しているかを知る必要があります。
・Producerは、対応できる作業をすべて出したことをConsumerに伝える方法が必要です。

このモデルを私たちの例に適用してみましょう。

<pre lang="ruby">
require 'thread'
require 'monitor'
require 'net/http'
 
# Our sample set of currencies
currencies = ['ARS','AUD','CAD','CNY','DEM','EUR','GBP','HKD','ILS','INR','USD','XAG','XAU']
 
# Set a finite number of simultaneous worker threads that can run
thread_count = 5
 
# Create an array to keep track of threads
threads = Array.new(thread_count)
 
# Create a work queue for the producer to give work to the consumer
work_queue = SizedQueue.new(thread_count)
 
# Add a monitor so we can notify when a thread finishes and we can schedule a new one
threads.extend(MonitorMixin)
 
# Add a condition variable on the monitored array to tell the consumer to check the thread array
threads_available = threads.new_cond
 
# Add a variable to tell the consumer that we are done producing work
sysexit = false
 
consumer_thread = Thread.new do
  loop do
    # Stop looping when the producer is finished producing work
    break if sysexit && work_queue.length == 0
    found_index = nil
 
    # The MonitorMixin requires us to obtain a lock on the threads array in case
    # a different thread may try to make changes to it.
    threads.synchronize do
      # First, wait on an available spot in the threads array.  This fires every
      # time a signal is sent to the "threads_available" variable
      threads_available.wait_while do
        threads.select { |thread| thread.nil? || thread.status == false  ||
                                  thread["finished"].nil? == false}.length == 0
      end
      # Once an available spot is found, get the index of that spot so we may
      # use it for the new thread
      found_index = threads.rindex { |thread| thread.nil? || thread.status == false ||
                                              thread["finished"].nil? == false }
    end
 
    # Get a new unit of work from the work queue
    currency = work_queue.pop
 
    # Pass the currency variable to the new thread so it can use it as a parameter to go
    # get the exchange rates
    threads[found_index] = Thread.new(currency) do
      puts Net::HTTP.get("download.finance.yahoo.com","/d/quotes.csv?e=.csv&f=sl1d1t1&s=USD#{currency}=X")
      # When this thread is finished, mark it as such so the consumer knows it is a
      # free spot in the array.
      Thread.current["finished"] = true
 
      # Tell the consumer to check the thread array
      threads.synchronize do
        threads_available.signal
      end
    end
  end
end
 
producer_thread = Thread.new do
  # For each currency we need to download...
  currencies.each do |currency|
    # Put the currency on the work queue
    work_queue << currency
 
    # Tell the consumer to check the thread array so it can attempt to schedule the
    # next job if a free spot exists.
    threads.synchronize do
      threads_available.signal
    end
  end
  # Tell the consumer that we are finished downloading currencies
  sysexit = true
end
 
# Join on both the producer and consumer threads so the main thread doesn't exit while
# they are doing work.
producer_thread.join
consumer_thread.join
 
# Join on the child processes to allow them to finish (if any are left)
threads.each do |thread|
    thread.join unless thread.nil?
end
puts "DONE!"
</pre>

この場合、リストに数百の通貨を追加しようとしても、システムに負担はかかりません。みなさんは、動作しているシステムを監視しながら、アプリケーションのパフォーマンスを最大限に引き出せるまで”thread_count”変数を調整したいと思うでしょう。

<h3>常に同じ結果が得られるように</h3>

スレッドを実行する時、みなさんにはもうコードが動作する順序はわかりません。ですから、共有しているストラクチャ（変数など）を変えるものはすべて、アプリケーションを矛盾した状態にする可能性があります。

コンソールにただ結果を書き込まず、あとで印刷できるように例を変更して共有配列に結果を書きましょう。

<pre lang="ruby">
require 'thread'
require 'monitor'
require 'net/http'
 
# Our sample set of currencies
currencies = ['ARS','AUD','CAD','CNY','DEM','EUR','GBP','HKD','ILS','INR','USD','XAG','XAU']
 
# Store our results here
results = Array.new
...
    # Pass the currency variable to the new thread so it can use it as a parameter to go
    # get the exchange rates
    threads[found_index] = Thread.new(currency) do
      # Add the results to the array
      results << Net::HTTP.get("download.finance.yahoo.com","/d/quotes.csv?e=.csv&f=sl1d1t1&s=USD#{currency}=X")
 
      # When this thread is finished, mark it as such so the consumer knows it is a
      # free spot in the array.
      Thread.current["finished"] = true
 
      # Tell the consumer to check the thread array
      threads.synchronize do
        threads_available.signal
      end
    end
...
# Show our downloaded currencies as they are stored in the array
puts results.inspect
puts "#{results.length} currencies returned."
puts "DONE!"
</pre>

アプリケーションを動作させて、どうなるか見てみましょう

<pre lang="cmd">
["\"USDCNY=X\",6.2254,\"12/7/2012\",\"4:14pm\"\r\n", "\"USDAUD=X\",0.9536,\"12/7/2012\",\"4:14pm\"\r\n", "\"USDCAD=X\",0.9905,\"12/7/2012\",\"4:14pm\"\r\n", "\"USDDEM=X\",0.00,\"N/A\",\"N/A\"\r\n", "\"USDARS=X\",4.8585,\"12/7/2012\",\"4:14pm\"\r\n", "\"USDEUR=X\",0.7735,\"12/7/2012\",\"4:14pm\"\r\n", "\"USDHKD=X\",7.7501,\"12/7/2012\",\"4:14pm\"\r\n", "\"USDGBP=X\",0.6234,\"12/7/2012\",\"4:14pm\"\r\n", "\"USDINR=X\",54.475,\"12/7/2012\",\"4:14pm\"\r\n", "\"USDUSD=X\",0.00,\"N/A\",\"N/A\"\r\n", "\"USDXAU=X\",0.0006,\"12/7/2012\",\"4:12pm\"\r\n", "\"USDXAG=X\",0.0303,\"12/7/2012\",\"3:33pm\"\r\n"]
12 currencies returned.
</pre>

13の通貨を要求したのですが、返ってきたのは12だけでした。もう一度動作させたら……今度は13の通貨が返ってきました。他に試したときも、12しか返ってこない時があります。なぜ結果がバラバラなのでしょうか？

問題は、子スレッドがすべて一つの配列（アレイ）にアクセスしていることにあります。2つ以上のスレッドがまったく同時に配列に結果を加える時、配列内の同じインデックスが指定されたところに複数のスレッドがアイテムを挿入するため、ひとつのスレッドが他のスレッドを上書きしてしまうことがあるのです。つまり、上記のコードを実行する時、返ってくる通貨の一つが上書きされてしまっていることがある、ということです。

この問題に対処するために、Mutexを追加することができます。Mutex「同期」ブロック内であるスレッドがコードを実行する時は常に、そのスレッドが配列に書き込む唯一のスレッドになるようにします。

<pre lang="ruby">
require 'thread'
require 'monitor'
require 'net/http'
 
# Our sample set of currencies
currencies = ['ARS','AUD','CAD','CNY','DEM','EUR','GBP','HKD','ILS','INR','USD','XAG','XAU']
 
# Store our results here
results = Array.new
 
# Create a mutex for the shared results array
results_mutex = Mutex.new
...
    # Pass the currency variable to the new thread so it can use it as a parameter to go
    # get the exchange rates
    threads[found_index] = Thread.new(currency) do
      # Add the results to the array
      results_mutex.synchronize do
        results << Net::HTTP.get("download.finance.yahoo.com","/d/quotes.csv?e=.csv&f=sl1d1t1&s=USD#{currency}=X")
      end
 
      # When this thread is finished, mark it as such so the consumer knows it is a
      # free spot in the array.
      Thread.current["finished"] = true
 
      # Tell the consumer to check the thread array
      threads.synchronize do
        threads_available.signal
      end
    end
...
puts results.inspect
puts "#{results.length} currencies returned."
puts "DONE!"
<pre>

上記のようにmutexを使うと、常に13の通貨が返ってくるようになりました。

<pre lang="cmd">
["\"USDARS=X\",4.859,\"12/7/2012\",\"4:15pm\"\r\n", "\"USDCNY=X\",6.2254,\"12/7/2012\",\"4:15pm\"\r\n", "\"USDCAD=X\",0.9905,\"12/7/2012\",\"4:15pm\"\r\n", "\"USDAUD=X\",0.9536,\"12/7/2012\",\"4:15pm\"\r\n", "\"USDDEM=X\",0.00,\"N/A\",\"N/A\"\r\n", "\"USDEUR=X\",0.7735,\"12/7/2012\",\"4:15pm\"\r\n", "\"USDGBP=X\",0.6235,\"12/7/2012\",\"4:15pm\"\r\n", "\"USDHKD=X\",7.7501,\"12/7/2012\",\"4:15pm\"\r\n", "\"USDILS=X\",3.8319,\"12/7/2012\",\"4:15pm\"\r\n", "\"USDINR=X\",54.475,\"12/7/2012\",\"4:15pm\"\r\n", "\"USDUSD=X\",0.00,\"N/A\",\"7:47am\"\r\n", "\"USDXAG=X\",0.0303,\"12/7/2012\",\"3:33pm\"\r\n", "\"USDXAU=X\",0.0006,\"12/7/2012\",\"4:15pm\"\r\n"]
13 currencies returned.
DONE!
</pre>

<h3>メモリの管理</h3>

短時間に多くのことを並行して行うアプリケーションを書くときは、メモリの使い方に注意しなければなりません。以下に、みなさんが陥りやすい落とし穴を挙げます。

<h4>メモリ膨張</h4>

膨張は、たいていの場合、メモリを戻さずにオブジェクトを詰め込み続けた時に発生します。Rubyのような言語では、この行為は常にオブジェクトを――おそらくハッシュまたはアレイなどを使って――「参照している」ことになります。この処理はますますメモリを増やす――「膨張させる」――ことになり、オペレーティング システムはあなたの処理の一部をスワップ（オーバーフローしたメモリ用のディスク パーティション、遅いです！）に動かさざるをえなくなります。利用可能なスワップ/RAMが全部使われてしまうまで「膨張」しつづけると、セグメンテーション違反、またはプロセスの終了などの望ましくない副作用がオペレーティング システムで発生します。

膨張を軽減する方法は、スレッド内にオブジェクトを確実に割当することです。マルチスレッドのアプリケーションでは、すべてのスレッドが親スレッドのメモリにアクセスできます。

この例では、アプリケーションをクラス機能に包みました。今は、通貨のアレイを得るために5分（300秒）ごとにループ内でそれを動作させています。

<pre lang="ruby">
require 'thread'
require 'monitor'
require 'net/http'
 
class CurrencyDownloader
  class << self
    def download_currencies
      # Our sample set of currencies
      currencies = ['ARS','AUD','CAD','CNY','DEM','EUR','GBP','HKD','ILS','INR','USD','XAG','XAU']
      ...
      # Show our downloaded currencies as they are stored in the array
      #puts results.inspect
      #puts "#{results.length} currencies returned."
      #puts "DONE!"
      # Return the results we downloaded
      return results
    end
  end
end
 
downloaded_currencies = Array.new
loop do
  Thread.new do
    downloaded_currencies << CurrencyDownloader.download_currencies
  end
  sleep(300)
end
</pre>

これは、みなさんが普通は書かない例を、わざと作り上げたものです。要は、後に続くスレッドがどのように動作するか、メモリがなくなるまでアレイがどのように増え続けていくかをお見せすることです。

では、メモリにもっと良心的にループを書き直しましょう。

<pre lang="ruby">
#downloaded_currencies = Array.new
loop do
  Thread.new do
    downloaded_currencies = Array.new
    downloaded_currencies << CurrencyDownloader.download_currencies
    # Perhaps do something with the results here...
  end
  sleep(300)
end
</pre>

各スレッドが終了する時、スレッド内に作られたストラクチャはゴミ集めができますから、今後のスレッドのためにメモリを解放し、「メモリ膨張」に対抗することができます

<h4>メモリ リーク</h4>

メモリ リーク(Memory leaks)は、メモリ膨張とはまったく違うもので、たいていの場合、こちらのほうが原因を突き止めるのが困難です。メモリ リークが発生している場合、アプリケーションはメモリ割当をしているのですが、何らかの理由でアクセス不可になっており、ガベージコレクタ（Garbage Collector：GC）によってバックアップを解放できなくなっています。

<h4>メモリ分析ツール</h4>

「漏れ口を塞ぎ」、どこでコードを最適化すべきかを発見するのに役立つツールやジェムがたくさんあります。

膨張しているところを突き止めるために私が発見した「間に合わせ」の方法は、以下のようなコードを使うことです。

<pre lang="ruby">
def get_object_stats
  return_value = Hash.new
  ObjectSpace::each_object(Object) {|my_object|
    unless return_value[my_object.class.to_s.downcase].nil?
      return_value[my_object.class.to_s.downcase][:count] += 1
    else
      return_value[my_object.class.to_s.downcase] = Hash.new
      return_value[my_object.class.to_s.downcase][:name] = my_object.class
      return_value[my_object.class.to_s.downcase][:count] = 1
    end
  }
  return_value.sort_by {|k,v| -v[:count]}
end
 
@thread_object_stats_logger = Thread.new do
  loop do
    break if @sysexit || expired?
    str_usage_report =  "OBJECTS IN MEMORY AT PID=#{Process.pid}\n"
    str_usage_report << "=============================================\n"
    get_object_stats.each do |stat|
       str_usage_report << "#{stat.at(1)[:count]}\t\t\t#{stat.at(1)[:name]}\n"
    end
    str_usage_report << "\n=============================================\n"
    info str_usage_report
    sleep 300
  end
end
</pre>

このコードは一定の間隔（この場合、5分間）で動作し、各タイプのオブジェクトのいくつが現在アプリケーションに割当てられているか目録を作ります。一つの動作から別の動作までの結果を比較する時は、割り当てられたオブジェクトの数が常に増え続けているオブジェクト クラスに注意してください。それが最適化すべきオブジェクトです。このコードはアプリケーションの経費を増やすため、製品内で動作させたくないコードです。しかし、みなさんはそれを「デバッグ モード」にしたり、コマンドライン スイッチで起動させたいと思うかもしれません。

このことを理解するのに特に役に立ったのは、Rubiniusチームが書いた記事です。この記事では、Rubiniusに組み込まれているツールを検討し、さらなる分析をするためのOS Xの「リーク」とgdbの使い方も説明しています。

Http://rubin.us/doc/en/tools/memory-analysis/

<h3>依存性を管理する</h3>

並行アプリケーションを書いている時は、ジェムとその他の依存性が必ず「スレッド セーフ」になるように書かれていることを確認してください。以下に、例をふたつ示します。

<h4>古いライブラリ</h4>

自分のOSライブラリとジェムがどのくらい新しいものかを知りましょう。新しいバージョンには、マルチスレッド アプリケーション用により最適化されたものがあります。Rubinius自体ですら、この分野では改良に励んでいるところです。

例えば、私は最近、API I用の SSL certificateが何度も繰り返し呼び出していたところで（リーク コマンドを使って）メモリ リークを見つけました。RubiniusをOpenSSL v1.0.1cで再コンパイルすることによって、このメモリリークは解消されました。

<h4>不必要な抽象化</h4>

抽象化レイヤは、アプリケーションを書くのに必要なコードの量を減らすかもしれませんが、経費を増やしてしまう可能性があります。例えば、弊社のアプリケーションのひとつで、私たちはスレッド セーフティとパフォーマンスの問題を追跡していました。そして、私たちの作成した、大量のデータをPostgresデータベースに挿入するジェムに原因を絞り込みました。同様のタスクを実行する他のジェムでは、そのような問題は起きていませんでした――このジェムと他のジェムとの違いは、この特別なジェムがpgジェムではなくORMを使ってPostgresとつながっていたことでした。ORMを取り除くと、アプリケーションのパフォーマンスは大幅に向上し、使用済みメモリの量が激減しました。

<h3>結論</h3>

この投稿から学んだことは、主に以下の通りです。

<ul>
<li>単にハードウェアで問題を解決しようとせずに、複数のものを同時に動作させる方法を探す。</li>
<li>並行処理と並列処理の違いをよく知っておく。</li>
<li>並行処理／並列処理したアプリケーションを本気で望むなら、適切なインタプリタを選ぶ。（Rubiniusを使いましょう！）</li>
<li>スレッドを使う時は……<ul>
<li>スレッドが実行されるのを見届けてから、アプリケーションを終了する。</li>
<li>Producer/Consumerモデルなどの制御メカニズムを使って、スレッドがただコンテキスト スイッチングを行っているのではなく、たいていは動作していることを確認する。</li>
<li>自分のスレッドで編集されるメモリ内のストラクチャを保護する――mutexかmonitorを使う。</li>
<li>アプリケーションがどのようにメモリを使っているのか意識すること。</li>
<li>必ずスレッドセーフのジェムを選ぶこと。</li>
</ul>
</li>
</ul>
これでパート1はおしまいです。パート2では、処理とキューイング メカニズム――スレッドが十分ではない時に使うオプション――について説明します。
