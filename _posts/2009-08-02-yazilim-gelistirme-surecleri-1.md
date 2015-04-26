---
layout: post
title: Yazılım Geliştirme Süreçleri - 1
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Yazılım geliştirme işinin hep acil olduğu, hesapsız kitapsız ve hallederiz gazları ile başlanan projelerin, sürecin tamamının kod yazmaktan(implementation) ibaret olmadığını bilse de öyleymiş gibi davranan bir ülkede geçirilen 10 yılıma üzülmemi sağlayan bir öykü paylaşacağım sizinle! Proje yöneticiliği yapan arkadaşların, bu süreçleri es geçip yıllarca önümüze sürdüğü bütçe palavraları üzerine bir yığın genelleme mevcut. Ama inanın hem bütçeyi doğru kullanmak, hemde işi kitabına uygun bir şekilde yapmak mümkün. Nasıl diye sorduğunuzu duyar gibiyim! <em>Süreçleri bir taşla on kuş vuracak şekilde düzenlemek</em> aslında söylediğim şey. Belgelemeyi PHPDocument ile yapmak gibi birşey aslında söylemek istediğim. Ve <em>ekibin enerjisini doğru bir şekilde yaymak</em>. İşin sırrı, her işe doğru adama atamak. Genelde Türkiye'de bir yazılımcı, sayfa tasarımdanda, DB tasarımından, güvenliktende, nesne yönelimli konulardan ve browser bağımsız javascript ve css hilelerinden haberdardır. Ve tüm enerjisiyle herşeyi çözer! Buradaki insanlara bundan söz ettiğimde, nasıl herşeyi bilmemizin beklediklerini anlayamadılar ve doğal olarak; nasıl öğrendiğimizi sordular!. Cevabım mı?; Halleluja Google! :)

Yeni görevim ve şirketimde geçen bir haftaya gelirsek, Ted ile bir hafta boyunca proje ekibi ile tasarım toplantıları yaptık. Proje ekibimizde bizim dışımızda; 2 frontend developer, 2 backend developer (biri aynı zamanda DB uzmanı), 1 sysadmin, 1 grafiker var.

İlk gün, müşteriden gelen RFP (Request For Proposal) belgesi baz alınarak çıkarılan StoryBoardları inceledik. Benden önce kullanılacak teknolojiye karar verilmiş, use-case diagramları Ted tarafından çıkarılmış ve ekip bu teknolojiye uygun olarak seçilmişti. Toplantı öğle yemeği saatine kadar sürdü ve projedeki herkes kendi açısından neler gerektiği ile ilgili notlar aldı ve deneyimlerini ekip ile paylaştı.

Öğleden sonra, frontend yazılım geliştiriciler, WADA (Wep Application Data Architect) adında, içerisinde isteklerin ne şekilde yapılacağını nasıl yanıtların alınacağı ile ilgili bir döküman hazırlamaya koyuldular. Dökümanda ayrıca template engine içerisinde kullanılacak veri atamalarıda yer alıyordu. Bu dosya JSON formatında olduğu içinde rahatlıkla versiyon takip sistemine eklenip değişiklikler hızlı bir şekilde yapılmasını hedefliyordu.

Ben ve Ted ise öğleden sonra, tasarım toplantılarına başlamıştık. Veritabanı uzmanı ile birlikte E/R diagramını hazırladık. Akşama kadar performans konuları (aktif/pasif, clustering) gibi konular konuşuldu.

Backend geliştiriciler ise, geliştirme ortamlarını sistem yöneticimiz Fabian ile birlikte hazırladılar, hangi kütüphaneleri kullanacakları vb konulara karar verdiler ve ertesi iki gün boyunca; Ted, ben ve 2 backend geliştiricisi ile birlikte, sınıf diagramları ve sekans diagramlarını tartıştık. Performans ve güvenlik konularının konuşulduğu bir toplantı olduğunu söyleyebilirim.

Üçüncü günün akşamında grafiker bize 3 taslak ile geldi. Bu toplantıya frontend geliştiricilerde katıldı. Buradada ağırlık kullanılabilirlik ve sayfanın yükü üzerine ve ajax düşünülen yerlerin etkileri üzerine yapılan konuşmalar vardı. Nerelerde cache kullanılması gerektiği gibi notları Ted not ettiğini gördüm. Bu bilgi anında eposta grubu ile paylaştırıldı. İşin ilginç tarafı bu tasarımlarla ilgili kimse güzel olmuş gibi yorumda bulunmadı. Benim dışımda, kimse tasarımın güzelliği ile ilgilenmiyordu. Bu toplantının gündemi kullanılabilirlikti ve beğenip beğenmediğini söyleyecek tek kişi ise müşteriydi. Toplantının yapılmasındaki amaç, tasarım müşteriye sunulmadan önce, frontend tarafında sonradan çıkabilecek kötü süprizler ve müşteriden gelebilecek saçma isteklerin önüne geçmekti.

Şirketin ortak bir zihni olduğunu söyleyebilirim. Zaten ilk geldiğim gün bundan söz etmişlerdi. Yazılan ve öğrenilen herşey, tüm şirket tarafından biliniyor ve hemen kütüphanedeki yerini alıyordu. Böylece tekrar tekrar pek birşey yapılmıyordu.

Cuma günü yaptığımız toplantıda draft olsalarda hemen hemen herşey hazırdı. Müşteri tasarımı seçmiş, sınıf diagramlarının büyük çoğunluğu hazırlanmıştı. Tüm sayfalar ve görünüm bileşenleri(widgets) sayfaların nasıl davranacağı, ne gibi görünüm bileşenelerine ihtiyaç olduğu WADA dökümanında belirtilmişti. Neredeyse herşey projenin 2. haftasında rayına oturmuş görünüyordu. İnanılmaz bir deneyimin parçası olmuştum.

Bu projedeki edindiğim deneyimlerimi paylaşmaya daha sonraki yazılarımda devam edeceğim. Sözünü ettiğim belgelerin örneklerini de izin alabilirsem buraya dahil edeceğim.
