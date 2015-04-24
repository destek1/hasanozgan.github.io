---
layout: post
title: PHP ve NoSQL (MongoDB)
tags:
- activemongo
- Diğer
- kohana
- linux
- mango
- mongodb
- morph
- nosql
- php
- symfony
- ubuntu
- zend
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  _oembed_ead9a72fc961f237b3994be6bb251750: ! '{{unknown}}'
  _oembed_1ff83bdbbf3147a069f4f011933cfe2c: ! '{{unknown}}'
  _oembed_15773043416760e4363ed4dc60ebaf28: ! '{{unknown}}'
---
<strong>NoSQL Nedir? </strong>
NoSQL, ilişkisel olmayan bir veritabanıdır. SQL dili kullanmadan Map-Reduce kavramı ile sorgulama yapılır. Map ve Reduce, aslında fonksiyonel programlamada sıkça kullanılan iki fonksiyondur. Excel buna güzel bir örnektir.

Gün geçmiyorki tarih tekerrür etmesin. NoSQL kelimesini birkaç blogta okuduğum vakit Yazılım Mimarı olan 40-45 yaşlarında bir büyüğüme bundan söz ettim. O da, aslında bunun yıllar önce kullanılan Berkley_DB'den başka birşey olmadığını söyledi. Berkley_DB aynı anda çalışan binlerce iş parçacığının(thread) 256 terabyte büyüklüğüde bir veritabanına erişebilmesini mümkün kılar. SQLite'ta BerkleyDB'ye benzer bir yapıya sahiptir. Ama biz SQLite'ı küçük işlerde kullanırız!. Biraz kafa karıştırıcı olduğunu biliyorum. Burada ilginç bir döngü var? Internet mozaik bir yapıdadır. Ve dağınıktır. Bu dağınık yapıyı Google'ın yaptığı gibi indekslemek (tabiri caizse tüm interneti indirmek isterseniz), dünyanın en büyük ve en iyi ilişkilsel veritabanını kanalize olmuş Oracle bile yetersiz kalacaktır.

<strong>Peki neden?</strong>
<ol>
	<li> İlişkisel veritabanları, yazma hakkı olan bir sunucu üzerinde koşar. Ana sunucuya birşey olması durumunda slave makinelerden biri master'a çevirilir ve yola devam edilir. Burada ki veritabanına gelen yazma isteklerini düşünebiliyor musunuz?</li>
	<li> Veritabanı büyüdüğünde yedekleme gibi işlemler (bakım) sorun olmaya başlar.</li>
	<li> Replikasyona dair sorunlar yaşayabilirsiniz.</li>
	<li> Google'ın 1 milyon makinesi olduğu varsayılıyor! Bu kadar makinelerin yarısının aynı anda tek bir makineye yazma isteği bulunduğunu düşünürsek durum daha net anlaşılabilir.</li>
</ol>
Google, startup döneminde, bir mühendislik şirketi gibi davrandı ve ihtiyaçlarını iyi analiz etti. 10.000$'lık sunucular almak yerine 500$'lık ucuz makineler satın aldı. Ve bu makinelerin kısa ömürlü ve her an patlayacağını bilerek kodlarını yazdı. Ve BigTable denilen (Hadoop bunun açık kaynak halidir) Map ve Reduce fonksiyonları ile sorgulamayı sağlayan bir mimari kurdu. Bu mimarinin en önemli özelliği; makinelerden biri göçse bile, sistemin çalışmaya devam etmesidir. Her kaydın 3-5 ayrı sunucuda kopyası bulunmaktadır. Bu şekilde web için en uygun devasa bir Mosaic oluşturdular.

Peki NoSQL konusuna giriş yaptık. Fakat bu seferde karşımıza birden fazla NoSQL türü çıkacak;
<ol>
	<li> Key/Value database (Redis, MemcachedDB vb..)</li>
	<li> Document Oriented database. (MongoDB, CouchDB)</li>
	<li> Object database (db4o)</li>
	<li> Graph databse (neo4j)</li>
	<li> Tabular (bigtable, hadoop)</li>
</ol>
Biz bu türlerden, belge yönelimli veritabanları konusu üzerinede duracağız. Belge yönelimli veritabanları, nesne yönelimli ve ilişkisel veritabanlarının alt katmanıdır. Yukarıda saydığım veritabanlarının birbirinden farkını ve merak ettiğiniz diğer konuları <a href="http://en.wikipedia.org/wiki/NoSQL">Vikipedi</a>'den okuyabilirsiniz. MongoDB'yi neden tercih ettiğime dair bilgilerine ise; <a href="http://www.mongodb.org/display/DOCS/Benchmarks">benchmark</a> testlerinden ve <a href="http://www.mongodb.org/display/DOCS/Comparing+Mongo+DB+and+Couch+DB">kıyaslama tablosundan</a> edinebilirsiniz.<!--more-->

<strong>MongoDB'yi Denemek İçin;</strong>
Eğer yukarıdaki bilgiler sizi tatmin etmedi ve MongoDB'yi biraz kurcalamak istiyorsanız ve zamanım yok makineye kurmadan denemek istiyorum diyorsanız; online olarak <a href="http://try.mongodb.org">şuradan</a> deneyebilmeniz mümkün.

<strong>MongoDB sunucusunun çalıştırmak için;</strong>
<pre lang="bash">mongod --dbpath=/data/mongo
</pre>
<strong>MongoDB'nin Ubuntu'ya Kurulumu</strong>
MongoDB'nin Ubuntuya nasıl kurulduğunu anlatacak olsamda diğer işletim sistemleri ve linux dağıtımlarına nasıl kurulacağını <a href="http://www.mongodb.org/display/DOCS/Quickstart">şuradan</a> öğrenebilirsiniz.
APTITUDE ile kurmak için; aşağıdaki dağıtımınız için uygun olan paket kaynak adresini seçerek <strong>/etc/apt/sources.list</strong> dosyasına kopyalamanız yeterlidir.
<pre lang="bash"># for Ubuntu Lucid (10.4) (built using a prerelease installation)
deb http://downloads.mongodb.org/distros/ubuntu 10.4 10gen

# for Ubuntu Karmic (9.10)
deb http://downloads.mongodb.org/distros/ubuntu 9.10 10gen

# for Ubuntu Jaunty (9.4)
deb http://downloads.mongodb.org/distros/ubuntu 9.4 10gen</pre>
ve sonrasında da aşağıdaki komutları çalıştırmanız yeterlidir.
<pre lang="bash">sudo aptitude update
sudo aptitude install mongodb-stable
# ya da
sudo aptitude install mongodb-unstable
# ya da
sudo aptitude install mongodb-snapshot</pre>
<pre lang="bash"># install dependicies for Ubuntu 9.04 ve 9.10
sudo apt-get -y install tcsh git-core scons g++
sudo apt-get -y install libpcre++-dev
                      libboost-dev libreadline-dev
                      xulrunner-1.9.1-dev

# get source
git clone git://github.com/mongodb/mongo.git
# build
scons
# install
sudo scons --prefix=/opt/mongo install</pre>
Görüldüğü üzere kurulum son derece basit. Derlenerek kurulum işleminde yapılması gereken başlangıç betiği hazırlamak.
<pre lang="ruby">#!/usr/bin/env ruby -w
# mongo ;; 2010 (cc) Jan Riethmayer
# This work is licensend under a Creative Commons Attribution 3.0 license.

require 'optparse'
options = {}

optparse = OptionParser.new do|opts|
  opts.banner = &lt;&lt;-BANNER
Usage: sudo ./mongo [options]
BANNER

  options[:dbpath] = "/data/mongodb/"
  opts.on( '-d', '--dbpath', 'Select DB path. Defaults to /data/mongodb/' ) do |path|
    options[:dbpath] = path
  end

  options[:port] = "27017"
  opts.on( '-p', '--port PORT', 'Listening to port 27017 by default' ) do |port|
    options[:port] = port
  end

  options[:fork] = false
  opts.on( '-f', '--fork', 'Run as daemon' ) do
    options[:fork] = true
  end

  options[:logpath] = "/var/log/mongodb.log"
  opts.on( '-l', '--logfile FILE', 'Defaults to /var/log/mongodb.log' ) do |file|
    options[:logpath] = file
  end

  opts.on( '-h', '--help', 'Display this screen' ) do
    puts opts
    exit
  end
end

# Parse the command-line. Remember there are two forms
# of the parse method. The 'parse' method simply parses
# ARGV, while the 'parse!' method parses ARGV and removes
# any options found there, as well as any parameters for
# the options.
optparse.parse!

class Go
  attr_accessor :opts

  def initialize(opts)
    @opts = opts
  end

  def start
    puts "Starting on port #{@opts[:port]} with dbpath #{@opts[:dbpath]}"
    puts "Running as Daemon" if @opts[:fork]
    puts "Writing to logpath /var/log/mongodb.log"
    path = "--dbpath #{@opts[:dbpath]}"
    port = "--port #{@opts[:port]}"
    log = "--logpath #{@opts[:logpath]} --logappend"
    fork = "#{@opts[:fork] ? '--fork' : ''}"
    params = [path, port, log, fork].join(" ")
    result = %x{ ./mongodb/bin/mongod #{ params } }
    puts result
  end

  def stop
    process = %x{ ps -o pid,command ax | grep mongod }
    found = false
    matcher = process.scan(/(\d+).+?bin.+?mongod.+?--fork/) do |pid|
      found = true
      puts "Killing process #{pid}"
      %x{ kill -2 #{pid} }
    end
    puts "No mongod process found" unless found
  end
end

go = Go.new(options)

case ARGV[0]
  when /start/ : go.start
  when /stop/ : go.stop
  else
  raise ArgumentError.new("mongo (start|stop) or mongo -h for help.")
end</pre>
Yukarıdaki dosyayı <strong>/etc/init.d/mongo</strong> şeklinde kaydetmek gerekiyor.

<strong>PHP Kurulumu</strong>
<pre lang="bash">sudo pecl install mongo
</pre>
PHP için monog eklentisinin hatasız bir şekilde derlenebilmesi için bilgisayarınızda <strong>phpize</strong> yüklü olmalıdır. Derleme işleminden sonra, php.ini dosyanıza;
<pre lang="ini">extension=mongo.so
</pre>
ekledikten sonra kurulum işlemi tamamlanmış olur.

Artık PHP mongo ile konuşabilecek durumda. PHP'nin sınıfları ile ilgi detaylı bilgiye <a href="http://tr.php.net/mongo">php.net/mongo</a> adresinden ulaşabilirsiniz.

PHPMyAdmin gibi bir yönetim arabirimi arıyorsanız, <a href="http://www.phpmoadmin.com/">PHPMoAdmin</a> tam size göre.

<strong>PHP Frameworkleri</strong>
Birçok popüler PHP framework'ünün MongoDB için ActiveRecord patternine uygun yazılmış eklentisi mevcut. Gelin bunlara bir göz atalım;
<strong>Zend Framework</strong>
<ul>
	<li><a href="http://framework.zend.com/wiki/display/ZFPROP/Zend_Nosql_Mongo+-+Valentin+Golev">Zend_Nosql_Mongo</a> Zend firması tarafından geliştirilen sınıf.</li>
	<li><a href="http://github.com/coen-hyde/Shanty-Mongo">Shanty Mongo</a> ise diğer bir sınıf.</li>
</ul>
<strong>CakePHP</strong>
<a href="http://github.com/ichikaway/mongoDB-Datasource/downloads">MongoDB Datasource</a> sınıfı.

<strong>Kohana</strong>
<a href="http://github.com/Wouterrr/mangodb">Mango</a> ise Kohana için ActiveRecord paternini kullanan bir sınıf.

<strong>Symfony</strong>
Symfony için Jason Mooberry tarafından yazılan makalenin, <a href="http://blog.jasonmooberry.com/2009/08/mongodb-and-symfony-yes-part-1-inserts/">1. bölümü</a> ve <a href="http://blog.jasonmooberry.com/2009/08/mongodb-and-symfony-yes-part-2-simple-queries/">2. bölümünden</a> bilgi edinebilirsiniz.

<strong>Kütüphaneler</strong>
<ul>
	<li><a href="http://github.com/crodas/ActiveMongo">ActiveMongo</a> güzel bir kütüphane. Bu kütüphaneye başlangıç yapmak için ise <a href="http://crodas.org/activemongo.php">şu makaleye</a> bakabilirsiniz.</li>
	<li><a href="http://code.google.com/p/mongodb-morph/">Morph Kütüphanesi</a></li>
</ul>
<strong>PHP ile İlgili Diğer Makaleler</strong>
<ul>
	<li><a href="http://technosophos.com/content/mongodb-5-things-every-php-developer-should-know-about-mongodb">http://technosophos.com/content/mongodb-5-things-every-php-developer-should-know-about-mongodb</a></li>
	<li><a href="http://www.businessinsider.com/how-we-use-mongodb-2009-11">
http://www.businessinsider.com/how-we-use-mongodb-2009-11</a></li>
	<li><a href="http://www.lafermeduweb.net/billet/nosql-mongodb-et-php-premiere-approche-781.html">http://www.lafermeduweb.net/billet/nosql-mongodb-et-php-premiere-approche-781.html</a></li>
	<li><a href="http://blog.boxedice.com/2009/07/25/choosing-a-non-relational-database-why-we-migrated-from-mysql-to-mongodb">http://blog.boxedice.com/2009/07/25/choosing-a-non-relational-database-why-we-migrated-from-mysql-to-mongodb</a></li>
	<li><a href="http://www.phpclasses.org/blog/post/118-Developing-scalable-PHP-applications-using-MongoDB.html">http://www.phpclasses.org/blog/post/118-Developing-scalable-PHP-applications-using-MongoDB.html</a></li>
</ul>
MongoDB gerçekten çok iyi belgelenmiş ve birçok web çatısı tarafından desteklenen harika bir araç. Bu konuda ki paylaşımlarınızı bekliyorum. :)
