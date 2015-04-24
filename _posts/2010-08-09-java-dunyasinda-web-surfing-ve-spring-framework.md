---
layout: post
title: Java Dünyasında Web Surfing ve Spring Framework
tags:
- Diğer
- ecplise
- hibernate
- java
- maven2
- sitemesh
- spring
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  jd_tweet_this: 'yes'
  wp_jd_target: http://javatar.bz/java-dunyasinda-web-surfing-ve-spring-framework/
  wp_jd_bitly: http://bit.ly/9sRVqj
  _wp_old_slug: ''
---
Scala dili ile tanıştığımda çok radikal bazı kararlar aldım. Java teknolojileri dışındaki tüm bildiğim teknolojileri (PHP, C#, Perl, Ruby) elimin tersi ile itme kararı aldım! Neden mi? Çünkü Java hem kariyer planım (Web Architect) için hem de mesleki tatmin anlamında oldukça güçlü bir platform ve ekosisteme sahip. Peki ha deyince yapılabiliyor mu derseniz, işte bu yaz onun hikayesidir.

Java'ya geçme kararı almadan önce Scala diliyle birşeyler yapmayı düşünüyordum. Lift framework'u falan incelemiş ve bazı özelliklerinden çok etkilenmiştim. Sonra <a href="http://kariyer.net" target="_blank">Kariyer.net</a> ve <a href="http://indeed.com" target="_blank">Indeed.com</a> üzerinde; <a href="http://liftweb.net/" target="_blank">Lift</a> ve <a href="http://scala-lang.org">Scala</a> ile verilen iş ilanlarına baktım. Scala ile şu anda para kazanamayacağımı anladıktan sonra, Java'nın gücünden faydalanmaya karar verdim ve Scala'yı özellikle Akka projesi ile distributed konularda kullanmaya karar verdim.

2006-2007 döneminde Turkcell'in <a href="http://turkcell-im.com">SDP-A</a> adlı projesinde çalışmamdan bu yana daha sonra çalıştığım şirketlerde Java teknolojilerine çok az sürmüş olmamdan kaynankalan bir gerileme söz konusuydu. Bu durumu kotarmak için, <em>"Sun Certified Java Programmer"</em> sertifikası alarak, hem kendime, hem de ekosistemine bilgimi ispat edeceğime karar verdim. Ekim ayının sonunda SCJP sınava gireceğim. Bunun için öncelikle Amazon'dan <a href="http://www.amazon.co.uk/Certified-Programmer-Study-Guide-CX-310-065/dp/0071591060">SCJP Study Guide</a> ve <a href="http://www.amazon.com/Java-TM-Puzzlers-Pitfalls-ebook/dp/B001U5VJVS/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1281388008&amp;sr=1-1" target="_blank">Java Puzzlers</a> kitaplarını sipariş ettim.

Tabii sadece sertifika sahibi olmak ve/veya diğer dillerden miras gelen kod geliştirme standartlarını (design patterns gibi) bilmek yeterli değildi. Java ekosisteminde kullanılan araçlarada hakim olmalıydım. Web üzerinde çalışmalar yapan biri olarak, Java dünyasının popüler web çatılarını incelemeye başladım. <a href="http://www.springsource.org/">Spring Framework</a>'ün adını çokca duymama rağmen, Java 6 ile tam uyumlu olan Jboss'un <a href="http://seamframework.org/">Seam framework</a>'ude ilgimi çekmişti ilk zamanlar. Sonra bu kararı kollektif yatırıma bıraktım, biraz araştırma yapınca Java ekosisteminde bir numara olan web çatısının açık ara spring olduğunu anladım. Bu nedenle Spring ile yoluma devam etmeye karar verdim.

Framework seçme işlemiyle aynı paralel zamanda IDE'de araştırmaya başladım. Maalesef Java öyle Vim ile yazmak işkenceye dönüşebiliyor. Önceleri IntelliJ Idea'yı sevsem de, ücretli olmasından ve her açılışta projeyi derinlemesine incelemesinden arayışa devam ettim. Netbeans'i denedim ama oldum olası ısınamamışımdır. Sonra eski dost Eclipse'e geri döndüm. Ve bugün IDE olarak tercihim <a href="http://eclipse.org">Eclipse</a>'ten yana oldu.

Derleme işlerinde ise eskiden Ant kullanan biri olsamda Maven2'yi tercih ettim. Maven ile tanışmam Scala daha doğrusu Lift framework vesile oldu. Paket bağımlılıkları ve deployment sürecini kolaylaştırması nedeniyle hemen kanım kaynadı. Archetype'lar sayesinde bir proje iskeleti hazırlamak çok kolay oluyor.

Spring framework'u seçtikten sonra, template engine armaya başladım. Önce Spring'te JSP örnekleri görünce ısınamadım. Ben JSF'teki gibi tag kütüphaneleri oluşturabileceğim bir template engine arıyordum. JSF ile Spring'i aynı çatıda kullanmayı denediysemde beceremedim. Daha sonra birşeyleri yanlış yaptığıma karar vererek durumumu tekrar inceledim. Ve JSP örneklerindeki JSTL teknolojisini keşfettim. JSTL tag libarary olmasına rağmen benim için yeterli değildi, layout yada master page gibi bir mimari içermiyordu. Araştırmalarım sırasında önce <a href="http://tiles.apache.org/">Apache Tiles</a> ile hedefe ulaştığımı düşünsem de, sonra <a href="http://www.sitemesh.org/">Sitemesh</a> ile bu işleri daha temiz bir şekilde çözelbildiğimi farkettim.

ORM ve Persistence aracı olarak tüm java kullanıcılarının tek geçtiği <a href="http://www.hibernate.org">Hibernate</a>'i kullanmaya karar verdim.

Son olarak güvenlik ve yetkinlendirme konularında <a href="http://www.acegisecurity.org">Acegi</a>, zaman ayarlı işler için ise <a href="http://www.quartz-scheduler.org/">Quartz</a> kullanmaya karar verdim.

Bir sonraki yazımda spring framework ve söylediğim araçların Maven kullanarak Spring çatısı altında nasıl entegre edeceğimizi konuşacağız. Tabii konularda ilerledikçe seviyemizi arttıracak ve vites büyülteceğiz.

Ama bu süreçte bana akıl hocalığı (mentor) yapan ve deneyimlerini sıkılmadan paylaşan değerli dostum <a href="http://rayyildiz.com">Ramazan Ayyıldız</a>a teşekkür ederim.

Java kocaman dalgaları olan bir derya. Ve bu dalgalarla surf yapmanın tadına doyulmayacağı aşikar. :)
