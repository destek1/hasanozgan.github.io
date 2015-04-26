---
layout: post
title: Yazılım Mühendisi'nin Şerefi
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Merhaba Üstad, biliyorum uzun süredir yazamıyorum. Son dönemde yazmak için çok okudum çok araştırdım ama yazmak için ataletimi yenemedim. Öğrendiklerimi yakın zaman içinde seninle paylaşacağım ama öncesinde yaşadığım bir şeyi paylaşmak isterim. Yıllar önce öğrettiğin temel şeylerin öneminin farkına galiba yeni vardım. Unutmamak ve öğrencilerine anlatman için bunu seninle paylaşmak istedim.

Yakın gelecekte, çaylakların yapmayacağı kadar basit bir hatam ve çok daha büyük bir sonucu oldu. Hatasız yazılım olmaz ama bu hatadan dolayı gerçekten çok utandım. Sonuçta şirketim, bozmak için değil yapmak için kodları bana emanet etmişti. Emanete hıyanet etmiştim. Samurayların böyle bir durumda Harakiri yaptıklarını çokça duymuşuzdur. Bu aslında daha iyi birine yol açmak için yapılır. En iyinin bile en iyisi vardır. Bunu hiçbir zaman unutmamak gerekir. Bu sebeple bende gereğini yaptım ve istifamı verdim. Fakat yöneticim bunu reddetti ve hatımın sebebini sorgulamamı istedi...

Profesyonel bir kurumda işinizi yapar ve karşılığınızı alırsınız. Bulunduğunuz pozisyondan dolayı kibir ve özgüveniniz gereksiz büyüyebilir ve basit hataları farketmemize engel olur. İşte bendeki en büyük sorun buydu. Bir yazılım geliştiricisi için en büyük tehlike fazla özgüven ve kibirdir. Çünkü diğer önemli kuralları gözden geçirmenize engel olur. Üstadım evet sende hiç kibir ve ego görmedim hiçbir zaman. Ama öğrencilerine ilk anlatman gerek şey bu olmalı. Yoksa benim yaşadığım utanç verici duruma düşebilirler.

Yazılım geliştiricisinin diğer görevlerini de, burada yazmak istiyorum. Bu maddelerin üzerine elbet eklentiler yapacağım ve/veya içinden bazı maddeleri çıkaracağım. Yol haritam olacak bu maddeleri bir daha unutmayacağım. Şimdi bu maddeleri burada tekrar hatırlayalım.

1) Alçak gönüllülük; bildiklerim denizde bir damla kadar ve daha öğrenilecek çok şey var ve biliyorum ki her zaman benden daha iyisi var. Kıstasım her zaman daha iyi olan olmalıdır.

2) Okunabilirlik (readibility); Yazılan kod herkes tarafından anlaşılabilir olamalı. Karmaşık kodlardan kaçılınılmalı. İsimlendirmeler öyle uygun olmalıki ne işe yaradıklar hakkında fikir vermeli. Yorum satırları olmalı. Kod standardına uygun yazılmalı.

3) Verimlilik (efficiency); Uygulamanın hızını yavaşlatabilecek hatalı algoritma ve mantıklardan kaçınılmalı. Method çağrıları 'profiler' araçları ile incelenmeli.

4) Nesnellik (objectivity);
<ul>
	<li>Yapısallık (structurally); Veri bütünlüğünü doğru bir şekilde parçalamak ve yönetmek için kullanılır. Doğru veri bloklarına doğru işler yapması sağlanabilir. İş parçalarını doğru yönetmek ve dağıtmak için iyi bir yöntemdir. Özellikle Handler mekanizmalarıyla hayata giren <em>"tek giriş ve tek çıkış"</em> sağlamak gibi tekniklerle.</li>
	<li>Bölümlere Ayırma (Modularity); Kod ilgilerine göre bölümlere ayrılabilmelidir.</li>
	<li>Tekrar Kullanılabilirlik; Kod tekrarı yapmak en büyük günahlardan biridir. Kodun tasarımında tekrar yapılması kesinlikle engellenmelidir.</li>
</ul>
6) Güvenlik (security); Güvenlik açığı oluşturulabilecek sorunlar tespit edilmeli ve kod içerisinde gereği yapılmalıdır. Güvenlik söz konusu olduğunda verimlilik ve hızdan bir miktar taviz verilmesi doğaldır.

7) Taşınabilirlik (portability); Uygulama; platform geçişlerine minimum değişiklik ile geçirilebilmelidir. Bunlara örnek, C kodlarındaki değişken veri tiplerinin uzunlukları ve işletim sistemine özel fonksiyon çağrıları verilebilir. Ya da uygulamada veritabanı değişikliğinde mevcut kodların en az seviyede etkilenmeside taşınabilirlik için iyi bir örnektir.

8) Esneklik (Flexibility); K.I.S.S. kuralına göre kod olabildiğince basit tasarlanmalıdır. Çevik yöntemlerse, geleceği düşünerek kod yazmak bir hatadır. Fakat bunu  düşünememek demek değişikliği yok saymak demek değildir. Bu sebeple uygulamanın kodları basit ve esnek olmalıdır.

9) Yeterlilik; Uygulamayı ve değişikliğin etkilerini iyi bilmek gerekir. Değişikliğin etkildeği yerler çıkartılabilmelidir.

10) Test edilebilirlik; TDD ile hayatın kod geliştirme döngüsünün içinde olmazsa olmaz bir parçası haline gelmiştir.

Benim temel ilkelerim bunlar üstadım; Eklemek ve düzeltmek istediğin birşey varsa sabırsızlıkla cevabını beklemekteyim.
