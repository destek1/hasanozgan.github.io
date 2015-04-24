---
layout: post
title: Sanal Pos Kütüphanesi
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  _wp_old_slug: ''
---
<p>Tüm dünyada da aynı mıdır bilmiyorum ama Türkiye'de düşünmeyi sevmeyen ve sıcak para gelsinde nasıl olursa olsun diye düşünen bir girişimci kitlesi vardır. Bu kitlenin müdavimlerini çeşitli şekillerde gördük ve görmeye devam edeceğiz elbette. Buna birkaç örnek vermek gerekirse; Sucular, İnternet Kafeler ilk aklıma gelenlerden birkaçı.</p>

<p>Birçok sektör gibi yazılım şirketlerinde de durum pek farklı değil. Türkiye'de her yazılımcı bir dönem Muhasebe yazılımları ile köşe olmayı düşünmüş ve bu alanda yazılımlar geliştirmiş ve sonunda batmıştır :) İşini hakkıyla yapan AirTies, SesTek, Sobee gibi şirketleri bunun dışında tutmak istiyorum tabii. Onlar gerçekten göğsümüzü kabartan güzel şirketler.</p>

<p>Bu durum internet sektöründe de neredeyse böyle. Internet'te dönemsel olarak popüler olan konular hep olmuştur. Şirket sitesi yapanlar, e-ticaret sitesi yapanlar bunun en büyük örneği. E-ticaret belkide en zahmetli ve uçtan uca hizmet vermeyi gerektiren, güvene dayalı olduğu düşünülürse fırsatlar ve riskler kendini hemen belli eden bir konu olduğu halde, en çok uğraş verilen ve yukarıdaki saydıklarım göz önünde bulunmadan girilen bir iş modeli.  E-ticaret bu yazının ana konusu değil, bu yüzden e-ticaretin sorunlarına bu yazıda değinmeyeceğim. Ama bu kadar çok üzerinde konuşulan, araştırmalar yapılan ürünler geliştirilen sektörde neden <a href="http://magentocommerce.com">Magento</a>, <a href="http://opencart.com">OpenCart</a> gibi açık kaynak projelerin Türkiye'den çıkmadığını merak ediyorum doğrusu!? Tamam bu çok büyük bir proje ama hazır yemeğe alışan bizler defalarca POS kütüphanesi yazdığımız halde bunu neden açık kaynak kodlarını yayınlamıyoruz?!</p>

<p>Türkiye'nin önde gelen birkaç e-ticaret platformunun altyapısını geliştirenlerden biri olarak bu soruyu kendime yönelttiğim de, en azından Türk yazılım camiasına böyle bir katkıda bulunmam gerektiğine karar verdim. İyimi ettim, kötü mü ettim zaman gösterecek elbette!. <a href="http://vpos4php.googlecode.com">Geliştirdiğim API</a> kütüphanesinin kullanıcı rehberi belgeyi yakında tamamlayacağım. Bu konuda ki gelişmeleri <a href="http://twitter.com/HasanOzgan">@HasanOzgan</a>(benim) ya da <a href="http://twitter.com/dahius">@dahius</a>'un twitter hesabından takip edebilirsiniz.</p>

<h6>Sanal Pos Kütüphanesi (<a href="http://vpos4php.googlecode.com">vpos4php</a>)</h6>

<p>Bu kütüphane aynı zamanda <a href="http://pear.php.net">PEAR</a> kütüphanesi hazırlamaya, paketlemeye, <a href="http://phing.org">Phing</a> ve <a href="http://phpdoc.org">phpDocumentory</a> kullanımı için bir örnektir. <a href="http://phpunit.de">PHPUnit</a>'de kullanımı ile ilgili örnekleri TestCase'lerinide ileride ekleyeceğim.</p>

<p>Türkiye'de Sanal POS altyapısını sunan 2 firma bulunmaktadır. EST ve POSNET. Birçok banka bu iki firmanın altyapısını kullanır. EST altyapısını kullanan bankalara Garanti, İşbankası, Axess, HSBC, Finansbank; POSNET altyapısını kullanan bankalara ise YapıKredi örnek verilebilir. Yani bu firmaların API'lerini kullanan her bankada bu kodlar çalışacaktır. Başka bir şirketin yaptığı altyapıyıda desteklemek için dökümanı bana gönderebilirsiniz.</p>

<p>Yapılan işlemler aşağı yukarı tüm POS altyapılarında aynı olunca bunları aynı veritabanları gibi tek bir arayüz üzerinden çalıştırmak gerekmektedir. İşte bunun için; projeyi geliştirilirken, tasarım kalıplarından(design patterns), fabrika (Factory Pattern) kullanılmıştır.</p>

<p>Kütüphane aşağıdaki methodları desteklemektedir.
<ol>
<li>
	<strong>provision</strong>($request) methodu, kredi kartından çekilen para miktarı, kart limitinden düşürülür. Ama hesabınıza geçmez. Bazı firmalar kart doğrulama gibi işlemler için bunu kullanırlar. Bankalar arasında farklılık gösterse de, eğer daha sonra <strong>disposal</strong>  methodu ile finanslaştırılmazsa tutarın kart üzerindeki blokesi kaldırılır. <br/>3D secure işlemi desteklenir. 
</li>
<li>
	<strong>sale</strong>($request) methodu, $request nesnesi içerisinde belirtilen tutar kredi kartı limitinden düşürülür ve hesabınıza geçer. <br/>3D secure işlemi desteklenir.
</li>
<li>
	<strong>disposal</strong>($request) methodu, daha önce <strong>provision</strong> methodundan geri dönen işlem numarası (transactionId) ile birlikte finanslaştırmaya yarar. Yani daha önce kart limitinizden düşürülen para hesabınıza geçer. 
</li>
<li>
	<strong>reversal</strong>($request) methodu, daha önce <strong>disposal</strong> ya da <strong>sale</strong> methoduyla finanslaştırdığınız işlemlerde kısmi iadeler yapmayı sağlar. Yani fiyatı güncelleştirebilirsiniz.
</li>
<li>
	<strong>refusal</strong>($request) methodu, daha önce yaptığınız bir işlemi iptal etmeyi sağlar.
</li>
<li>
	<strong>complete</strong>($request) methodu ise, 3DSecure işlemlemini tamamlamayı sağlar.
</li>
</ol>
</p>

<p>Bu api ile ilgili her türlü sorularınızı bana yöneltebilirsiniz. Fırsat buldukça size yardım etmeye çalışacağım.</p>

<p><a href="http://vpos4php.googlecode.com">vpos4php</a> kütüphanesinin proje sayfasına <a href="http://code.google.com/p/vpos4php/downloads/list">buradan</a> indirebilirsiniz.</p>
