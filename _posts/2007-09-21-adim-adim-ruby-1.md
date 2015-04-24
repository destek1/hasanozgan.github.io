---
layout: post
title: Adım Adım Ruby  - 1 -
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Ömrüm boyunca "C sytax"(C++, PHP, Java, C#, JS) dillerde geliştirmeler yaptım ve onları öğrendim. Bu nedenle <a href="http://www.ruby-lang.org">Ruby</a>'i kabullenmek ve sindirmek benim için çokta kolay olmadı. Lakin, <a href="http://www.ruby-lang.org">Ruby</a>'in özelliklerini görünce tüm ön yargılar, yerini eğlenceli bir oyuncağa bıraktı. Ruby öğrenme sürecimi bu kategori altında sizlerle paylaşacağım. Şimdi bakalım ilk adım ne olmalı?

<strong>Neden Ruby'i Seçmeliyim ?</strong>
<a href="http://www.ruby-lang.org">Ruby</a>, son birkaç yılda <a href="http://www.rubyonrails.org">Ruby on Rails</a> ile popülerlik kazanan bir dil. Henüz <a href="http://www.python.org">Python</a> gibi çok geniş bir kütüphane arşivine sahip değil! Ama yakın gelecekte bu açığın doldurulacağına hiç şüphe yok. <a href="http://www.ruby-lang.org">Ruby</a> bir betik (script) dili. Ve betik dillerinden beklenen en önemli özelliğe sahip. Çeviklik ! Aşağıda bazı ilgi çeken özelliklerini size fikir vermesi için yazacağım. Not: Bu özelliklere detaylı olarak bir sonraki yazımda "programlamaya yeni başlayanlara" anlatır gibi beraber göz atacağız. C'de böyle Java da şöyle gibi notlarımı da aralara serpiştireceğim elbette.

Ne diyorduk? <a href="http://www.ruby-lang.org">Ruby</a> çok amaçlı bir dil olsa da günümüzde özellikle web uygulamalarının geliştirilmesinde kullanılıyor. Web uygulamalarında tercih edilme sebeplerinden biri anında sonucu görebilmeniz. Yani Java'daki gibi derle bak, aptal uygulama sunucusunu yeniden başlat gibi absürdlükler yok!. ASP.NET 2.0 ile beraber, Java'daki bu salak mimariye alternatif olarak <strong>App_Code</strong> gibi bir özellik gelmiş durumda. Tabii katmanlı mimariye geçtiğiniz an oda aynı şekilde derleme vs. gerektiriyor. (Tabii binary kütüphanelerin şöyle bir avantajı var. Kütüphane yazan proje ekibinin kodunu kullanan ekibin kafasına göre kod değiştirmesine engel oluyor. Böylece versiyon ve kod tabanı dağılmamış tek bir ekibin hakimiyetinde oluyor. Neyse konumuz bu değil gerçi ama aklıma gelmişken ileteyim dedim.

Bunca laf ebeliği yaptıktan sonra, benim neden <a href="http://www.ruby-lang.org">Ruby</a>'i seçtiğimi söyleyeyim. Web uygulamamın Linux sunucunda koşmasını istiyorum. C# dilini seviyorum ama maalesef Mono hala sinir olmadan yazabileceğiniz bir durumda değil! <a href="http://www.ruby-lang.org">Ruby</a>, Python gibi zorlayıcı özellikleri yok. Özellikleri ile kod yazarken eğlenmenizi sağlıyor. Çok hızlı gelişen bilişim sektöründe, aklınıza gelen fikrin, en hızlı şekilde ürüne dönüşmesi için, her projede muhakkak yaptığımız tekrarları <a href="http://www.rubyonrails.org">Ruby on Rails</a> framework'unun engelliyor olması.

<strong>Nereden Başlamalı ?</strong>
Bilgisayarınıza <a href="http://www.ruby-lang.org">Ruby</a>'i indirerek başlayabilirsiniz! :-) <a href="http://www.ruby-lang.org">Ruby</a>, P3OS (Popüler 3 İşletim Sistemi: Windows, OSX, Linux)'ı destekler! <a href="http://www.ruby-lang.org">Ruby</a>'i kodlarını denemek için <strong>irb</strong> uygulamasını kullanabileceğiniz gibi windows kurulum paketinde gelen SCiTE editorunude kullanabilirsiniz. <a href="http://www.ruby-lang.org">Ruby</a>'i bilgisayarınıza kurduktan sonra, Mark Slagell tarafından yazılan, <a href="http://www.pinguar.com">Pınar Yanardağ</a> tarafından güzel türkçemize kazandırılan <a href="http://www.belgeler.org/uygulamalar/ruby/ruby-ug.html">Ruby Kullanıcı Klavuzu</a> dökümanını okumanızı öneririm. Genel bir bakış yapmanızı ve <a href="http://www.ruby-lang.org">Ruby</a>'e olan ön yargıları yıkmanıza ve ilk adımı hızlıca yapmanızı sağlayacağı gibi aşağıda önereceğim kitaplar için bir ön hazırlık olacaktır.

<a href="http://www.ruby-lang.org">Ruby</a>'e bir giriş yapıp ne olduğunu öğrendikten sonra <a href="http://www.ruby-lang.org">Ruby</a> on Rails'i indirebilir ve Rails ile denemeler yapmaya başlayabilirsiniz. Rails ile ilgili denemeler için tavsiyem, şu <a href="http://www.digitalmediaminute.com/article/1816/top-ruby-on-rails-tutorials">eğitmene (tutorial)</a> bakmanızı öneririm. Eğer genel <a href="http://www.ruby-lang.org">Ruby</a> hakkında daha fazla bağlantı arıyorsanız <a href="http://del.icio.us/search/?p=ruby">buradan</a> bulabilirsiniz..

Rails'i terminalden şablon kodları generate ederek kullanabileceginiz gibi bir tüm platformlarda çalışabilen IDE'ler yardımıyla da kullanabilirsiniz. Ruby için, Eclipse eklentilerinin yanı sıra, Eclipse üzerine inşa edilmiş Aptana isimli JS IDE'sinin eklentisi olarak duyurulan Rad Rails'i kullanmanızı öneririm. Eğer Netbeans kullanmayı seviyorsanız Netbeans 6.0 ile Ruby desteği geldiğini söylemeliyim. Söylememe gerek var mı bilmiyorum ama, Vim ve Emacs ile Ruby yazmanız da mümkün!

<strong>Ne Gibi Özellikleri Var ?</strong>
<em>Mantıksal İşlemler: </em>
Ruby denetleyicileri ile biraz Perl'ü anımsatsa da, benim özellike ilgimi çeken <strong> === </strong> operatörü. Bu operatör ile bir sayıyı aralığını tek hamlede kontrol edebiliriz.
<blockquote><strong>irb(main):001:0&gt; </strong> i = 4
<strong>irb(main):002:0&gt; </strong> (2..5) === i

=&gt; true<em></em></blockquote>
<em>Yordamsal Nesneler: </em>
Bu özelliği C'deki fonksiyon göstericilerine (function pointer) benziyor. Yada C#'taki temsilci (delegate)'ler gibi çalışıyor. Bir kod kümesini bir yordam(process) icine alarak, daha sonra çağrı yapabilirsiniz.
<blockquote><strong>irb(main):001:0&gt; </strong>deamon = proc{ print "Deamon çalıştı \n" }
<strong>irb(main):002:0&gt; </strong>deamon.call

=&gt; Deamon çalıştı</blockquote>
<em>Tekil Metodlar: </em>
Bu metod modeli, bir sınıfın bir metodunun geçici olarak yeniden yazılmasını sağlayan bir özellik. Bu özelliği kullanabilmek için sınıfın nesnesinin yaratılması gerekiyor.
<blockquote><strong>irb(main):001:0&gt; </strong>class SingleMethod
<strong>irb(main):002:0&gt; </strong> def size
<strong>irb(main):003:0&gt; </strong> print "25\n"
<strong>irb(main):004:0&gt; </strong> end

<strong>irb(main):005:0&gt; </strong>end<strong></strong>

<strong>irb(main):006:0&gt; </strong>test1 = SingleMethod.new
<strong>irb(main):007:0&gt; </strong>test2 = SingleMethod.new
<strong>irb(main):008:0&gt; </strong>print "25\n"
<strong>irb(main):009:0&gt; </strong>def test1.size
<strong>irb(main):010:0&gt; </strong> print "10\n"
<strong>irb(main):011:0&gt; </strong>end

<strong>irb(main):012:0&gt; </strong>test1.size
=&gt; 10

<strong>irb(main):013:0&gt; </strong>test2.size
=&gt; 25</blockquote>
Bir sonraki yazımda daha detaylı olarak Ruby'nin özelliklerini anlatacağım. Bu girdiyi bazı bağlantı önerileri vererek sonlandırıyorum. Beni izlemeye devam edin efenim :p

<strong>Yazılımlar</strong>
<a href="http://www.ruby-lang.org/en/downloads/">Ruby</a>
<a href="http://rubyforge.org/">Ruby Forge</a>
<a href="http://www.rubyonrails.org/down">Ruby on Rails</a>
<a href="http://www.radrails.org/download_rails_rdt.php">Rad Rails</a>

<strong>Kitaplar</strong>
<a href="http://www.urlshield.net/l/nNX0NMJA">Learn to Program</a>
<a href="http://www.urlshield.net/l/DD5sUVsV">Programming Ruby</a>
<a href="http://www.urlshield.net/l/FgOQhKL">Agile Web Development with Rails</a>
<a href="http://www.urlshield.net/l/07IDsBrA">Rails Recipes</a>
