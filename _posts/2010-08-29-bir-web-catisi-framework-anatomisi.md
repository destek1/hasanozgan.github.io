---
layout: post
title: Bir Web Çatısı (Framework) Anatomisi
tags:
- acegi
- Diğer
- ehcache
- framework
- hibernate
- ioc
- java
- jsp
- jstl
- log4j
- maven
- mvc
- quartz
- thymeleaf
- sitemesh
- spring
- tiles
- url-rewrite
- webflow
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  _wp_old_slug: ''
---
2 yıldır PHP diliyle, <a href="http://code.google.com/p/joy">Joy</a> isimli açık kaynak bir framework geliştiriyordum. Bu framework’e Joy adını vermemin başlıca nedeni, uygulama geliştirken gerçekten zevk vermesini istememden kaynaklanıyordu. Bu framework’un 5 farklı versiyonu mevcut ve hepsinde de farklı yaklaşımlar kullandım. İlk versiyonu Event Driven patterni kullanırken, sonraki sürümlerde MVC patterni ağırlıklıydı. Event driven yapısı ise sonraki sürümlerde Workflow amacıyla yaşam döngüsünde yerini almıştı.

Bu sure zarfında çok şey öğrendiğimi itiraf etmeliyim. Birkaç ay once, piyasada çok fazla başarılı framework olması nedeniyle bu amacımdan vazgeçtim. Web dünyasının distributed computing ve parallel programming gibi konularada ihtiyaçlarınıda göz önünde bulundurarak, PHP yerini, JAVA’ya bıraktı ve Java projelerimin vazgeçilmez aracı olarak yerini aldı.

Java’yı projelerimin merkezine yerleştikten sonra, bu ekosistemde, <a href="http://code.google.com/p/joy">Joy Framework</a>’unde kullandığım fikirlerin sağlayacak araçları aramaya koyuldum. İlk zamanlar kaygılarım olsada J2EE ve Spring framework çevresinde aradığım herşeyi buldum. Aşağıda bu fikirleri ve Java dünyasındaki araçları bulacaksınız.
<div class="maddeler">
<ul>
	<li>URL Rewriter</li>
	<li>Router (Dispatcher)</li>
	<li>Core
<ul>
	<li>Config Management</li>
	<li>Log Management &amp; Debugging</li>
	<li>Cache Management
<ul>
	<li>Distributed Cache</li>
	<li>Locale Cache</li>
</ul>
</li>
</ul>
</li>
	<li>Controller
<ul>
	<li>Filter</li>
	<li>Workflow</li>
</ul>
</li>
	<li>Context
<ul>
	<li>Culture</li>
	<li>User</li>
	<li>Request</li>
	<li>Response</li>
	<li>Session</li>
</ul>
</li>
	<li>View
<ul>
	<li>Render</li>
	<li>Template Engine</li>
	<li>Tag Library</li>
</ul>
</li>
	<li>Model
<ul>
	<li>ORM</li>
	<li>Persistence</li>
</ul>
</li>
	<li>Plugin
<ul>
	<li>Geolocation vb...</li>
</ul>
</li>
	<li>Tools (Extra)
<ul>
	<li>Console Tool
<ul>
	<li>Code Generator</li>
	<li>Deployment</li>
	<li>Builder</li>
	<li>Documentation</li>
</ul>
</li>
	<li>Testing</li>
	<li>Inversion of Control</li>
	<li>Scaffolding</li>
	<li>Scheduler</li>
	<li>Authentication &amp; Authorization
<ul>
	<li>OAuth</li>
	<li>LDAP</li>
</ul>
</li>
	<li>Client Side Library
<ul>
	<li> Javascript (jQuery)
<ul>
	<li>Cache</li>
	<li>Cookie</li>
	<li>Hotkeys</li>
	<li>Lazy Including</li>
	<li>Querystring</li>
	<li>Comet</li>
	<li>AJAX</li>
</ul>
</li>
	<li> CSS Frameworks
<ul>
	<li>960gs, Blueprint</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</div>
Yukarıda sözünü ettiğim konuları PHP ile  birçoğunu geliştirdim. xUnit, ORM , Library gibi kapsamlı konular için ise 3<sup>rd</sup> parti araçları kullandım. Bu yönüyle Integrated Framework olarakta adlandırılabilir.

Hayatımın 2 yılı bu yapı üzerinde uygulamalar geliştiriken Java’ya geçince bir boşluğa düştüğümü ve paniklediğimi itiraf etmeliyim. Neyse ki Spring Framework ve Java’nın Servlet mimarisi beni ciddi rahatlattı. Java dünyasının üstadları yukarıdaki konularda daha once benim yerime kafa yormuş ve düşündüğüm birçok şeyi hayata geçirmişti. Şimdi gelin bu teknolojilerin neler olduğuna bir göz atalım. Sonrada Java’nın ve Spring’in gücüyle bir web çatısı nasıl olur onun güzel bir örneğini inceleyelim.
<div class="maddeler">
<ul>
	<li><a href="http://www.oracle.com/technetwork/java/index-jsp-135475.html">Java Servlet</a>
<ul>
	<li><a href="http://java.sun.com/products/jsp/">JSP</a> ve <a href="http://www.oracle.com/technetwork/java/index-jsp-135995.html">JSTL</a></li>
</ul>
</li>
	<li><a href="http://www.springsource.org">Spring</a>
<ul>
	<li><a href="http://static.springsource.org/spring/docs/2.0.x/reference/mvc.html">MVC</a></li>
	<li><a href="http://static.springsource.org/spring/docs/2.0.x/reference/beans.html">Inversion of Container</a></li>
	<li><a href="http://static.springsource.org/spring-security/site/index.html">ACEGİ (Spring Security)</a></li>
	<li><a href="http://www.springsource.org/webflow">Web flow</a></li>
</ul>
</li>
	<li><a href="http://hibernate.org">Hibernate</a></li>
	<li><a href="http://wiki.sitemesh.org/wiki/display/sitemesh3/Home">SiteMesh</a>, <a href="http://tiles.apache.org/">Tiles</a></li>
	<li><a href="http://quartz-scheduler.org/">Quartz Scheduler</a></li>
	<li><a href="http://logging.apache.org/log4j/">Log4J</a></li>
	<li><a href="http://maven.apache.org/">Maven</a></li>
	<li><a href="http://ehcache.org/">EhCache</a></li>
	<li><a href="http://www.tuckey.org/urlrewrite/">UrlRewrite</a></li>
</ul>
</div>
Gelin şimdi yukarıdaki Java araçlarını yakından inceleyelim.

<strong>Java Servlet:</strong>
1.0 sürümün, JSR-315 diye adlandırılan 3.0 sürümüne kadar birkaç özellik dışında yaşam döngüsü pek değişmedi. Bu yaşam döngüsü, servlet mimarisinin esnekliğinin ana kaynağıdır. Web.xml dosyası içinde, Listener, Filter, Servlet tagleri bir web projesindeki tüm gereksinimleri kapsar. Frameworkler ise buradaki mimariden faydalanarak bu işleri daha kolay bir hale getirir. Şimdi gelin bu taglerin ne anlama geldiğini bir hatırlayalım.
<ul>
	<li><strong>Listener:</strong> Uygulama deploy edildiğinde ve undeploy edildiğinde burası çalışır. Isteklerden bağımsız olarak çalıştırılması düşünülen alanlar için düşünülmüştür. Örneğin; görev tanımlı işler için kullanılabilir. Quartz isimli scheduler'ın listener sınıfları vardır. Cache mekanizması içinde bu alan düşünülebilir. Yine EhCache uygulamasınında listenerları bulunmaktadır.</li>
	<li><strong>Filter:</strong> Filter tüm Request, Response trafiğinin arasına giren adında anlaşılacağı üzere filtreleme işlevi gören sınıflardır. Filterlara örnek olarak, Spring Security, ve Url Rewrite verilebilir.</li>
	<li><strong>Servlet:</strong> Response'un yaratıldığı alandır. Bu nedenle bir MVC framework'te genelde burada Router (Dispatcher) sınıfı bulunmaktadır.</li>
</ul>
<strong>Java Server Pages:</strong>
JSR-245 spesifikasyonunda detayları açıklanmıştır. JSP, PHP veya ASP'ye benzer. HTML üzerinde Java kodlarının çevik bir şekilde kodlanarak kullanılması amaçlanır. JSP dosyaları arkada otomatik olarak servlete dönüştürülür. Frameworkler ile birlikte, JSP dosyaları, template engine'i gibi kullanılmaya başlanmıştır.

<strong>Java Standard Tag Library:</strong>
Java'nın tag kütüphanesidir. Aynı ASP.NET'te olduğu gibi yeni bileşenler yaratılabilmesi sayesinde kod tekrarı engellenir ve yeniden kullanılabilirlik sağlanır.

<strong>Spring Framework:</strong>
Java dünyasında elinizi sallasanız bir Web Framework'e çarparsınız. O kadar fazladır ki, artık bıkkınlık getirir. Hangisini kullanmalı diye araştırıldığında, Spring Framework en çok tutulan frameworklerin başında gelmektedir. Bunun en önemli nedenlerinin başında, IoC, AOP gibi konuları sayesinde OOP ve tasarım prensiplerine uygun, bakımı kolay, temiz kodlar yazmamızı sağlaması gelmektedir. Struts'ı koltuğundan etmiş, Java EE 6'ya, getirdiği yeniliklerle ilham vermiş $ukella bir frameworktür. Kendi içinde, Security, Webflow, MVC vb gibi alt projeleri vardır. Sadece web alanında kullanmasa da, özellikle hakim olduğu alan burasıdır. VMWare tarafından desteklendiğini de belirtmekte yarar var.

<strong>Spring MVC:</strong>
Web dünyasının son moda tasarım şablonu olan MVC'nin Spring implementasyonudur. İşleri anotasyonlar kullanılarak, XML konfigürasyonlar en aza indirgenir. Zaten bir IoC konteynerı olması nedeniyle. Model ve View alanında alternatif teknolojilerle entegre olması mümkündür. Bu da teknoloji seçimi esnekliği sağlar.

<strong>Spring Security:</strong>
Spring Security, ACEGi olarakta bilinen bir projedir. Authentication ve authorization konularında çözümler sunar.

<strong>Spring Web flow:</strong>
İş akışlarını, kod bağımlılığını en aza indirgeyerek, XML konfigürasyonları ile yapılmasını sağlar. Bunun için event driven bir mimari kullanır.

<strong>Hibernate:</strong>
JBoss'un geliştirdiği bir numaralı Persistence aracı olan Hibernate'i bilmeyen yoktur sanırım. Kısaca DAO tasarım şablonunu destekler. Ve veri erişim katmanı mimarsi ile veritabanı tablolarını sınıflar ile eşleştirir.

Alternatif olarak ise Java EE 5 ile hayatımıza giren JPA adlı bir başka persistence aracıda bulunmaktadır. Java EE 6 ile birlikte daha çok göreceğimiz persistence aracıdır.

<strong>Sitemesh:</strong>
Çok yeni olmasına rağmen, her geçen gün daha fazla ilgi görmeyi başaran bir şablon motorudur(templete engine). Java dünyasında, bir framework seçildiğinde, özellikle bu framework, Spring gibi integrated bir framework ise, layout(master page)  ihtiyacı ile ilgili bir arayış söz konusu olur. İşte Sitemesh, Tiles ve Velocity bu durumlarda en çok başvurulan şablon motorudur. Açıkçası, ilk önce ilgimi Tiles çekse de, sonraları Grails projesininde katkılarıyla Sitemesh ilgileri üzerinde topladı diyebilirim. Sitemesh, Tiles'tan daha basit olması diğer bir tercih nedenidir. Decorator Design patternini kullanır. Bunun anlamı, layout sayfanızda, sadece değiştireceğiniz alanları belirler ve ilgili sayfalara sadece bu alanları değiştirirsiniz.

<strong>Quartz Scheduler:</strong>
Web dünyasında mutlaka, bazı işleri arkada düzenli olarak kontrol eden, yaratan vb servislere ihtyaç vardır. Örneğin, mail gönderme, statu güncellme vb.. İşte bu gibi konularda schuder bir servis gereksinimi var olur. Fakat iş mantığını ve birçok yardımcı kod java kodumuzdadır. Ve bu Cron gibi bir servise bağlandığında her seferinde bir VM'in belleğe yüklenip, kaldırılması anlamına gelir. Bunu engellemek için Servlet mimarisinde listener kullanmak daha yerinde olur. Çünkü Listener'lar aynı bellek alanını kullanır. Bu sayede ciddi bir performans kazanımı sağlanır.

İşte bu nedenle Quartz yaratılmıştır. Quartz trigger modelleri sayesinde, Cron benzeri bir formatta da konfigüre edilebilmektedir.

<strong>Log4J:</strong>
Apache projesinin loglama mimarisi.

<strong>EhCache:</strong>
Son zamanlarda, frameworkler gibi çok fazla cache projesi ortaya çıkmıştır. Bunların çok azı distirbuted bir yapıda çalışır ve clustered, replication gibi konuları destekler. Ehcache ise, distributed cache desteklmesi, memory yetersiz olduğu durumlarda diski kullanması (SWAP) gibi özellikleri sayesinde, en çok tercih edilen bir cache projesi olmuştur.

Java'da memcache gibi Java dışında bir dil kullanılarak yazılan cache motorlarının kullanılmamasının en önemli sebebi, In Memory kavramıdır. Ehcache, uygulama ile aynı memory alanında çalışması ciddi bir performans artışı sağlamaktadır.

<strong>Maven:</strong>
Maven, hem derlemek, hem de bağımlılıkları yönetmek için kullanılan çok kapsamlı bir deployment aracıdır. Derlemek işinin sadece bir bölümüdür. Bağımlılıkları yönetmenin yanında proje iskeleti konfigürasyon yaratmak konusunda da hünerleri vardır.

Diyelim ki, Spring MVC, Tiles ve Hibernate'i birlikte kullanmak istediniz ve konfigürasyonları ile uğraşmak istemiyorsunuz. <a href="http://code.google.com/p/spring-maven-archetype/">http://code.google.com/p/spring-maven-archetype/</a> projesi işinizi görebilir. Maven üzerinde birçok archetype projesi bulabilirsiniz. Ya da kendi archetype'nızı yazarak yeni bir projeye hızlı bir başlangıç yapabilirsiniz.

<a href="http://code.google.com/p/archy/">AppFuse</a> adında birçok alternatif teknoloji konfigürasyonunu içinde barındıran bir archetype projeside mevcuttur.

<strong>Not: </strong>Son olarak söylemek istediğim bir şey daha var, yukarıdaki bir çok teknolojinin entegre edilmiş ve çevik bir web programlama ortamı sağlayan framework daha var. Java VM ile çalışmasına rağmen kodları Java değil. Gördüğüm en iyi web frameworklerinden biri olan bu framework'ün adı <a href="http://www.grails.org/">Grails</a>. Yine arkasında <a href="http://springsource.org">Spring</a> ekibi var ve Spring'in birçok teknolojisi ustaca kullanılmış. Dil olarak ise <a href="http://groovy.codehaus.org/">Groovy</a> adında Ruby benzeri bir dil kullanılıyor. Groovy bir Java standardı. Java'nın gücüyle çevikliğin hızını birleştirmek isteyenler için küçük bir bilgi olsun istedim!

Artık elimizi koda bulamanın zamanı geldi. Yukarıdaki teknolojiler ile ilgili örneklere sırasıyla önümüzdeki yazılarda detaylı olarak ve örnekler sunarak inceleyeceğiz.
