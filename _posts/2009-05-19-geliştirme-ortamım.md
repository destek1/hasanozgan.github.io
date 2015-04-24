---
layout: post
title: Geliştirme Ortamım
tags:
- code-complete
- Diğer
- goto-decleration
- linux
- php
- test
- vim
- xdebug
- xinc
status: draft
type: post
published: false
meta:
  _edit_last: '2'
---
İşlerden, güçlerden birazda tembellikten yazamadım üstadım. Projeler projeler diyordum ya sana, tek tek yayına giriyorlar. Hayatımın en önemli kararlarını ve eylemlerini şu 6 ay içerisinde aldım ve de yaptım belki de. Hayal kırıklıklarım da oldu hayallerini yıktıklarım da.

Uzun süredir üzerinde çalıştığım, framework'ten ve üzerinde kullandığım mimarilerden söz etmek isterdim bu yazımda. Ama öncesinde geliştirme ortamımdan ve kullandığım betik dilden söz etmek ve aynı dili konuştuğumuzdan emin olmak istiyorum. (bknz: tereciye tere satmak) Elbette kullandığım teknolojileri ve tasarım kalıpları (pattern) bilinen uygulanmış yöntemler. Ben nasıl bir yenilik getirdiğim ise çok yakında diyerek geliştirme ortamımı anlatmaya geçeyim.

Bildiğin üzere üstadım, geliştirme ortamım ve aynı zamanda sunucu ortamım performans, güvenlik, maliyet kriterlerimden aldığı iyi notlar ve programcı dostu olduğu için <strong>Linux</strong>'tan yana oldu. Linux ile bir uygulama veya bir eklenti kurmak çalıştırmak ve/veya derlemek çok kolay. Bu kolaylıkları sağlayan Linux dağıtımım ise <strong>Debian</strong> mimarisi üzerine kurulan "İnsan İçin Linux" dağıtımı hazırlayan <strong>Ubuntu</strong>. Aklımdayken, senin önerin ile Mac OS X'i PC'me kurdum ama kendimi pek özgür hissedemedim. Belki MacOS'u bir Apple bilgisayar üzerinde denemediğimdendir ama yinede Linux'ta ki özgürlüğün ve esnekliğin gerçek tadı. Ve ben bunu seviyorum.

Geliştirme yaptığınız diller konusuna pek girmek istemiyorum. Ne de  olsa hepsi bizi amaca götüren araçlar. Biliyorum siz python seversiniz üstadım ama benim Web Mimarisi örneklerim genellikle PHP ile olacak. :) Sizin örneklerinizinde python ile olduğu gibi. PHP-GTK ile bir masaüstü uygulaması yazabilseniz de varlık sebebi Web'tir. Ve ilklerden olmanın en büyük avantajı ise üzerinde bu konuda biriktirdiği deneyimleridir. Özellikle PHP 5.3'ten sonra çok daha eğlenceli bir dil olacağını şimdiden söyleyebilirim. Siz ne dersiniz üstadım?..

<strong>Vi iMproved</strong>

Bunca kelâm ettikten sonra nihayet asıl konuya gelebildim, Metin Editorleri. Editorler konusunda söylenecek çok fazla şey var elbette. Ama benim tercihim <strong>Vim (Vi iMproved)</strong>'den yana olmuştur. Vim birçok özelliği olan harika bir metin editoru. Grafiksel arabirimde çalışan versiyonlarıda mevcut. Eklentiler ile istediğiniz her kıvama sokabilirsiniz. Bazı editorler<strong>*</strong> gibi, "ne iş olsa yaparım abi" modunda bir editor degildir!. Vim'in iddiası, "konusunda en iyisi benim, yeter ki aklını kullan!.." olmuştur.

Peki Vim ile neler yapabiliriz? Bit text editör'den beklediğinizi ve belki birazda fazlasını yapabilirsiniz. Başlıcaları şöyle sıralayabiliriz;
<ul>
	<li>Kopyala, yapıştır</li>
	<li>Ara, bul, değiştir</li>
	<li>Bulduklarını işaretle.</li>
	<li>Fare ile kullan</li>
	<li>Kod bloklarını aç veya kapa.</li>
	<li>Satır numaralarını göster.</li>
	<li>Aynı ekranda parçalar halinde kodları göster.</li>
	<li>Tablar halinde dosyaları aç.</li>
	<li>Makrolar tanımla.</li>
	<li>Yeni eklentiler ile Vim'i daha güçlü bir hale getir.</li>
	<li>Tab'a basarak kodu tamamlama.</li>
	<li>Fonksiyonun tanımlandığı yere gitmesi.</li>
	<li>Çalışma ortamındaki dosyaları ağaç şeklinde görebilme.</li>
	<li>Git, Subversion ve CVS ile entegre çalışabilme.</li>
</ul>
ve aklıma gelmeyen daha yüzlerce özellik. Sizin için bu özellikleri şurada bir araya topladım. Test ettim ve çalıştırdım. Bu geliştirme ortamına sahip olmak için yapmanı gereken sırasıyla aşağıdaki adımları takip etmek.

<strong>XDebug &amp; WebGrind</strong>

<strong>Firefox</strong>
