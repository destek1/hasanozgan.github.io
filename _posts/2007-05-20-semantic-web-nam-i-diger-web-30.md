---
layout: post
title: Semantic Web (Nam-ı Diğer Web 3.0)
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
<div style="text-align:center;"><em>"Web için bir hayalim var; bilgisayarlar, web üzerindeki tüm veriyi (içerikler, bağlantılar ve insanlarla bilgisayarlar arasındaki işlemler), analiz etme kabiliyetine sahip olacaklar. Henüz hazır olmasa da 'Semantic Web'in  yapılması mümkün!. Hazır olduğunda ise günden güne ticaret yöntemlerimiz, bürokrasi ve günlük yaşamlarımız birbiri ile konuşan makinalar tarafından idare edilecek. İnsanlığın asırlardır konuştuğu 'zeki araçlar' gerçek olacak."</em>
<div style="text-align:right; padding-right:25px;"><a href="http://tr.wikipedia.org/wiki/Tim_Berners-Lee">Tim Berners-Lee</a></div>
<img src="files/weblog/W3c_semantic_web_stack.jpg" alt="semantic web roadmap" /></div>
Söz büyüğündür der atalarımız, bu nedenle lafıma, internetin babası, semantic web kavramını ilk ortaya atan ve gerçekleşmesi için bir <a href="http://www.w3.org/DesignIssues/Semantic.html">yol haritası</a> bize sunan üstad <a href="http://tr.wikipedia.org/wiki/Tim_Berners-Lee">Tim Berners-Lee</a> ile başlayalım istedim. Geçtiğimiz yıl Web 2.0'ı anlamaya ve kavramaya çalışırken, geçen Kasım(Kasım 2006) ayında Web 3.0 adıyla yeni bir kavram duyduk. Neymiş bu Web3.0 dediğimizde eski bir terim ile semantic web kavramı ile karşılaştık. Aşağıdaki grafikte Web 4.0'ın bile adının geçtiğini dikkatinizi çekmek isterim. O da ayrı bir makale konusu olduğundan lafı çok uzatmadan neymiş bu semantic web gelin beraber inceleyelim.
<div><a href="http://farm1.static.flickr.com/250/452486876_b61b9ff7b2_o.jpg" target="flickr"><img src="files/weblog/webdevelopment.jpg" border="0" alt="" /></a></div>
<strong>Semantic Web nedir?</strong>

Web 1.0' da sayfalar insanların okuyup anlayabileceği şekilde hazırlanıyordu. Web 2.0 ile verileri etiketlemeye ve AJAX tekniği ile web sayfaları kullanımı kolay ve hızlı bir hal aldı. Makinelerin birbirleri ile konuşabilmesi için XML çıktılar veren metodlar ürettik. SOAP ve benzeri protokoller inşa ettik. Tim Berners Lee'nin telafuzunu ettiği Web 3.0’a geçiş için  gerekli olan hazırlıkları yaptık. Başında 'e' harfi koyarak bürokratik işleri bizim için makinalarin yapmasını sağladık. Bu makinaların konuştuğu yerlerde karar gerektiren noktalara ise insanlar koyduk. Web 3.0 ile makinalar bizi daha önceki davranışlarımızdan ve konuştuklarımızdan anlamaya ve çözümler üretmeye çalışacak. Makina-Makina ile karar gerektiren kısımlarda da konuşabilecek. Bu konuyu aşağıdaki gibi bir örnek ile açıklama çalışayım.

<em>Hayal edin!, diyelim ki cumartesi günü basketbol maçı yapacaksınız ve basketbol maçı yapmak için bir yer arıyorsunuz. Arama motoruna "istanbul'da cumartesi günü uygun basketbol sahası" şeklinde bir arama yaptınız. Arama motoru cümleyi yorumladı ve size sadece basketbol sahalarının bulunduğu siteleri getirdi. Hatta istanbul kriterinide girdiginiz icin sadece Istanbul'dakileri sahaları getirdi. İşte size semantic web budur. Semantic web zayıf bir yapay zeka kullanır. İşi biraz yokuşa sürelim ve yapay zeka kavramını devreye sokalım. Arama motoru hava durumunu inceleyip, cumartesi günü İstanbul'da yağış olduğu için sizi uyararak üstü açık olan basketbol sahalarını görmek isteyip, istemediğimi sorabilir. Yada sadece üstü kapalı basketbol sahalarını listeleyebilir. İşte yapay zeka ile semantic web arasındaki fark budur. </em>

Bu örnekten sonra gerçekleşmesi için neler gerektiğine bakalım.

<strong>Peki makinalar, siteleri bizim gibi nasıl anlayacak?</strong>

Makinaların bizi anlaması için gerçekten çok fazla veriye ihtiyaç var. İnternette bu veriler yeterli oranda mevcut. Fakat dağınık ve hiçbirinin bir diğerine makinaların anlayabileceği bir ilişkisi yok. Yani verilerin toplanması ve yorumlanması ve daha sonraki sorgulamalar için depolanması gerekiyor. Şimdi bu 3 temel öğe altında neler yapılıyor yada yapılması gerekiyor onları inceleyelim.

<strong>1) Verileri Anlamlı Bir Şekilde Ayrıştırma</strong>
<div style="padding-left: 20px"><strong>a) Etiketleme Yöntemiyle İçeriği Toplamak:</strong>

Web 2.0 ile beraber, hayatımızda etiketleme(tag) kavramı ortaya çıktı. Böylece makinaların bir sürü veri içinden biz insanlar için öncelikli ve gerekli olan bir veri alanı oluşturmuş olduk.  Etiketlemenin en büyük avantajı, kelimeler arasındaki ilişkilerin insanlar tarafından sağlanıyor olması. Mesela, kartal resimlerinin bulunduğu bir siteyi etiketlemek istesek, etiketimiz sanırım “kartal kuş fotoğraf ” gibi bir etiketler dizisine sahip olurdu.  Böylece sizin botlarınızın yapacağı işi insanlar yapmış olacak. %20’ye %80 kuralını bilirsiniz. Web üzerindeki verinin %20’si gerçekten insanların ihtiyacı olan veridir. Geri kalan %80 ise çöp veridir. Buna dayanarak, insanların girdiği veri tamamiyle %20’lik olan gerekli alana girecektir. Etiketlemek, aynı dizideki etiketlere göre bir anlam ilişkisi bulunur. Yukarıdaki örneğimizi ele alalım. Kartal bir kuştur. Ve sitedeki veriler kuş resimleridir. Çok güçlü olmasada kendimize küçük bir semantic web uygulaması oluşturduk. Tabii daha yapılması gereken çok iş var. Bu sadece bir başlangıç olduğunu unutmamak gerekir.

Etiketleme ile ilgili araç-amaç ilişkisine şuan aklıma gelen en güzel örnek, <a href="http://images.google.com/imagelabeler/">Google Image Labeler</a>. Google'ın amacı etiketi olmayan resimleri etiket altında toplamak. Ama bir sürü etiketlenmesi gereken resim var. Bu iş için nasıl bir şey yapmalı? İnsanlar eğlenceyi sever. Oyunlar eğlencelidir. Neden bu işi oyun olarak sunmayalım düşüncesi ile ortaya çıkmıştır.

<strong>b) Alana Göre İçeriği Toplamak:</strong>

Daha öncede söylediğim gibi semantic web için büyük bir içerik gerekli. Google'ın veri madenciliği yapmasının sebebi bu aslında. Google'ın hedefi, Hakia gibi semantic web. hatta belki daha da ileriye giderek yapay zeka (Google'ın Master Plan'ın çizili olduğu kocaman <a href="http://undergoogle.com/tools/GoogleMasterPlan.html">yazı tahtasını</a> incelemiş olanlar "AI Developer" hayallerini bilirler.) konuları. Fakat Google, Hakia’dan farklı olarak taklit ederek öğrenme yöntemini izliyor. Belli bir alana (domain) yönelik çıkardığı servisler bu amaca hizmet ediyor. İsterseniz bu servislerden bir kaçına bakalım;

<img src="http://www.ozgan.net:8086/files/weblog/googlemasterplan.jpg" alt="" />

1) GMail; epostaların hayatımıza girmesi ile çok önemli veriler, eposta kutularımızda toplanmaya başladı. Üye olduğumuz  yerler (ilgi alanlarımız)  ve şifreleri, özel yazışmalarımız, konuşama şeklimiz vs.. Neden google'ın bir dosyayı silmenizi istemediğini 2.8 GB alan verdiğini düşünüyorsunuz. Hatırlarsanız gmail ilk çıktığında davetiye yolu ile çalışıyordu. Yani insanların birbiri ile olan ilişkilerinide tutmakla işe başladılar.

2) GTalk; eğer bir bot yazacak olsanız. Dünyada bir çok insanın, sorulara karşı verdiği cevapları loglasanız ne elde ederdiniz. Birçoğumuz konuşurken çeşitli hazır kalıpları kullanırız.

- Naber

- İyilik, senden

Bu kalıp ve benzeri kalıpları sürekli kullanıyoruz. GTalk Google için inanılmaz bir insanı taklit aracı.

3) Google Image Labeler; oyun görünümlü servis. Web kullanıcıları bedavaya veri girişi için kullanamanın en etkili yolu :)

<strong>c) Anlamlı İndeksleme ve Dilbilgisi:</strong>

Hakia’dan yola çıkmak bu konu başlığı için çok doğru olacak. Yahoo ve Google’ın pagerank algoritması verileri kelime anlamına göre indekslemez. Metaya göre indeksler. Bu nedenle yukarıda söylediğimiz alana gore içerik toplama yöntemiyle ilerliyorlar. Anlamlı indeksleme için ise özellikle Google’ın çalışmaları olduğunu site çeviri servisi gibi bazı servisler bize ipucu veriyor.

Hakia’nın çalışmaları veriyi anlamlandırarak indeksleme temeline dayanıyor. Özellikle yaptıkları <a href="http://labs.hakia.com/hakia-lab-onto.html">OntoSem</a> (<a href="http://www.ontologicalsemantics.com/">Ontological Semantics</a>) adındaki teknolojileri bu işe yarıyor.  OntoSem, Prof. Victor Raskin’in akademik çalışması; bu konunun amacı doğal dilleri anlamlandırma temeline dayanıyor. Yani doğal diller üzerinde işlemler yazılım mühendisliğine dayanıyor.
Bu ciddi zorlukları olan bir konu. Cümle öğelerine bölünerek anlamlandırıldığı gibi tipine görede bir ontology ağacında yerini alıyor. Böylece kelimeler ağaçtaki yerine gore indeksleniyor. Yapay zekanın önemli konu olacağı şüphesiz bir konu. Hakia’nın diğer çalışmalarına <a href="http://labs.hakia.com/">buradan</a> erişilebilir.</div>
<strong>2) Ayrıştırılan Verilerin Bir Yerde Toplanması</strong>

Verileri toplamak için en yaygın yöntem olarak, RDF kullanılmaktadır. <a href="http://www.w3.org/RDF/">RDF(Resource Description Framework)</a> W3C’ bulduğu bir ilişkilendirme çatısıdır. Şimdiden birçok kurum ve kuruluş tarafından standart olarak kabul edilmiş ve kullanılmaya başlamıştır. Dilbilgisindeki özne, nesne, yüklem bağlantısına benzeyen bir söz dizimine sahiptir.

Yukarıda daha önce verdiğimiz örneğe geri dönersek; İstanbuldaki basketbol sahalarını listelemek. İTÜ, İstanbul’un en güzel basketbol sahasına sahiptir. Burada ‘İTÜ’ özne, ‘İstanbul’ nesne, ‘en güzel basketbol sahasına sahiptir’ ise yüklemdir. Şimdi bunu RDF içinde görelim.
<div style="padding-left: 50px">&lt;rdf:RDF

xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"

xmlns:dc="http://netology.org/dc/elements/1.1/"&gt;
&lt;rdf:Description rdf:about="http://etkinlik.itu.edu.tr/basketbol"&gt;

&lt;dc:location&gt;İTÜ&lt;/dc:location&gt;

&lt;dc:city&gt;İstanbul&lt;/dc:city&gt;

&lt;/rdf:Description&gt;

&lt;/rdf:RDF&gt;</div>
http://netology.org/dc/elements/1.1/ adresinde location ve city tanimlanmistir.

<a title="RDF Resource Description Framework" href="http://www.w3.org/RDF/">
<img src="http://www.w3.org/RDF/icons/rdf_w3c_icon.96" border="0" alt="RDF Resource Description Framework Icon" /></a>

Yukarıdaki örnekten de anlaşılacağı üzere RDF karışık bir yapıya sahiptir. Bu sebeple  <a href="http://www.w3.org/TR/owl-features/">OWL(Web Ontology Language)</a> kullanılmaktadır. OWL ontology grupları oluşturmaya yarar ve RDF'ten çok daha kolaydır. Aşağıda yaşlı kadınların sahip olduğu kediler ile ilgili bir örnek verilmiştir.
<div style="padding-left: 50px">Class(a:old_lady complete

intersectionOf(a:person a:female a:elderly))

Class(a:old_lady partial intersectionOf(

restriction(a:has_pet allValuesFrom (a:cat))

restriction(a:has_pet someValuesFrom (a:animal))))

Class(a:cat_owner complete intersectionOf(a:person

restriction(a:has_pet someValuesFrom (a:cat))))</div>
<ul>
	<li>Yaşlı kadınlar muhakkak evcil bir hayvana sahiptir.</li>
	<li>Yaşlı kadınların evcil hayvanları kedilerdir.</li>
	<li>Kedilerin sahibi yaşlı kadınlardır.</li>
</ul>
Daha kapsamlı bir örneğe <a href="http://www.cs.man.ac.uk/~horrocks/ISWC2003/Tutorial/">buradan</a> erişebilirsiniz.

<strong>3) Anlamlı Verilerin İçinden Sorgulama</strong>

SPARQL en çok kullanılan sorgulama dilidir. Hakia'nında bu konuda kendi geliştirdiği <a href="http://labs.hakia.com/hakia-lab-qdex.html">QDEX(Query Detection and Extraction)</a> adında bir teknoloji ile bu işi yapar.

<strong>Semantic Web İçin Başlangıç Noktası Neden Arama Motorları?</strong>

İnsanların hayatında her zaman büyük yada küçük bir hedefi vardır. Hedeflere ulaşmak için çeşitli <strong>çözüm <span style="text-decoration: underline;">ararlar</span></strong>. İşte anahtar kelime bu, <strong>Aramak</strong>. Hayatımız hep birşeyler arayarak geçer. Bir insanın 3 tip hedefi vardır.

a) İhtiyaç

b) Statü

c) Eğlence

Arama motorları neden hayrına bize böyle bir hizmet sağlıyor? Neden böyle bir amaçları var. Arkasında ne yatıyor olabilir? İnsanların aradıklarını bulmak için ne aradıklarını bilmeniz gerekir. İnsanların istedikleri şeyleri bildiğinizi düşünün. Bu tanrısal bir erdemdir. Ve gerçekten büyük bir güçtür. Çünkü bazı isteklerimizi, başkalarının öğrenmesi vicdanen bizi rahatsız edebilir. Sorumuza tekrar geri dönelim; neden böyle bir hizmet için mücadele ediyorlar?

Bence gelecekte bilgi hür olacaktır. Şu an çok saçma bir şekilde DNA'larımız, bazı hastalıklar patent altına alınmakta, birilerinin mülkiyeti altına girmektedir. Çeşitli fikir mülkiyetleri orta atılmaktadır. Bu fikri yıkmak adına CreativeCommon adı altında bir oluşum bulunmaktadır. Fikir mülkiyeti saçma bir fikirdir. Hepimizin bulduğu şeyler çevremizdeki etkenler ve duygularla yaratılmıştır. Bilgi kimseye ait değildir. Şuanki kapitalizm etkisindeki dünyanın bu fikri kabul etmesi güç olduğu muhakkak. Fakat düşünün bundan 20 yıl önce Richard Stallman özgür yazılım felsefesini ortaya attığında da insanların bu görüşü kabul etmesi pek kolay olmadı.

Peki arama motorlarının amacı yukarıda saydıklarımız mı dersiniz? Eğer ellerindeki tüm bilgiyi herkese açacaklarsa evet amaç bilgi özgürlüğü denebilir. Ama bu işlerle uğraşanlar akademik kurumlardan daha çok ticari kuruluşlardır. Ve hepsinin bir gayesi bulunmaktadır.

<strong>Tehlikenin farkında mısınız?</strong>

Gelecekte hepimizin bir profili olacak! Şu an kullandığımız kredi kartları, cep telefonları yada çeşitli internet servislerinde bu profiller yavaş yavaş oluşuyor. Nereden hangi ihtiyacımızı alıyoruz, nerelere gidiyoruz. Hepsi kayıt altına girmeye başladı Köleliğin formları değişmeye başladı. Artık birkaç beton yığını ile örülü değiliz. Akıllarımız köleleştiriliyor. Pazarlamacılar(marketing) Semantic Web konusuna yakından takip ediyor. Ağızlarının suyu akıyor. Bu insanlardan bilgiyi korunmanın yollarını aramak, bu kurumlara karşı özgür projelerle kırmaya çalışmak gerekiyor.

Yukarıda söylenilenler daha çok ütopik ve komplo teoriler içeriyor. <a href="http://www.albinoblacksheep.com/flash/epic">EPIC 2015</a>'te benzer bir durumdan söz ediyor. Ama gerçek payı yok mu? Bunu yapmayacaklarını kim iddaa edebilir.

Internette kişisel bilgilerimizi içeren birçok küçük servis mevcut. Göze çarpanlar Google, Yahoo gibi devler tarafından satın alınıyor. Bu bilgilerde devlerin veri madenlerine katılıyor. Peki hepsini almak mümkün mü? Elbetteki hayır. İşte Yahoo tarafından önerilen çözüm. Mashup'lar. Mashup, melez servislerdir. Birkaç servisin birleşmesi ile ortaya çıkar. Bu   fikir çok güzel olmakla birlikle, şirketlerin özgür yazılım felsefesinin onlar için zehirli olan tarafını atıp, açık kaynak adı altında yumuşatarak nasıl bedava insan gücü elde ettilerse, aynı şey mashup fikri ile bu küçük servislerin altyapılarını açmalarına zorlayacaktır.

<strong>İnternet Yaşamdır</strong>

Kurucusu olduğum <a href="http://www.netology.org">Netology Yazılım Vakfı</a>, internetin yaşamımızdaki  vazgeçilmez yerinin farkında olan bir oluşum. İnternetin tamamen kamu yararına kullanılması için yeni teknolojiler geliştirmeyi hedeflemektedir. Yakında bu konudaki çalışmalarımızı <a href="http://www.netology.org">http://www.netology.org</a> adresinden duyuracağız.

Üstadlar (<a title="Türk Dil Kurumu'nun internet üzerindeki sözlüğüne göre bu kelimenin anlamı 'Bilgisayar ve haberleşme teknolojileri konusunda bilgi sahibi olan, bilgisayar programlama alanında standartın üzerinde beceriye sahip bulunan ve böylece ileri düzeyde yazılımlar geliştiren kişi' olarak tanımlanır." href="http://tr.wikipedia.org/wiki/Hacker">hackers</a>) tarafından bugünkü halini alan intenet; şuan özgür olduğumuz ve global dünya fikrinin gerçekleştiği tek yer. Onu <a href="http://tr.wikipedia.org/wiki/Pazarlama">kimsenin</a> kötü emellerine alet edip kirletmesine izin veremeyiz.

İnternet yaşamdır ve bir devletin yada kuruluşun değil tüm kamunun malıdır!
