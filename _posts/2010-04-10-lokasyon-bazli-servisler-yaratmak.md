---
layout: post
title: Lokasyon Bazlı Servisler Yaratmak
tags:
- Diğer
- geolocation
- html5
- ip2location
- latitude
- longitude
- mysql
- php
- radius
- search
- zipcode
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Son 2 yıl içerisinde Mikro-blogları ve bu konuda geliştirilen web uygulamalarının adını çokça duyduk. Bu yıl ise, özellikle lokasyon bazlı uygulama örneklerini görmeye başladık. Foursquare, Loopt, Google Latitude, Gowalla, Rummble ve bu işe yeni girişen Twitter, Facebook aklıma gelen ilk örnekleri. (Ben bu yazıyı hazırlarken; Yahoo, FourSquare'ı satın almayı düşünüyor fakat 100 Milyon$ edip etmeyeceğine karar vermeye çalışıyordu)

Lokasyon bazlı servisler gizlilik konusunuda beraberinde getirdi. Hatta bu konuda Google'ın CEO'su Eric Schmidt'in '<a href="http://www.theregister.co.uk/2009/12/07/schmidt_on_privacy/">Gizlenmek istemeniz, gizlenmesi gereken işlerle meşgul olduğunuz anlamına gelir</a>' demecine en güzel cevabı, "Lütfen beni soyun" anlamına gelen ve foursquare'daki bulunduğunuz konuma göre hırsızlara davetiye çıkaran, <a href="http://PleaseRobMe.com">PleaseRobMe.com</a> isimli bir sitenin verdiğini düşünüyorum. Halen gizlilik politikaları lokasyon bazlı servislere karşı önyargıları olan insanları tatmin ettiği söylenemez.

Gizlilik konusu daha çok tartışılacak bir konu gibi görünüyor. Bunun en son örneği ise Fazlamesai.net sitesindeki <a href="http://www.fazlamesai.net/?a=article&amp;sid=5399">"Kim? Ne zaman? Kiminle? Nerede?"</a> başlıklı yazısı.

Bu tartışmalar süre dursun, lokasyon bazlı servisler artık hayatımıza girdi ve çıkacak gibide durmuyor. Peki bu işin teknik altyapısında neler var, gelin bunları inceleyelim ve bu blogun amacına uygun bir davranış sergileyelim.<!--more-->

<strong>Lokasyon Bazlı Servisler (LBS) Nedir? </strong>
Bir kişinin lokasyon bilgisini almanın birkaç yöntemi vardır. Bunlar;
<ul>
	<li>IP'den Lokasyon bulma (GeoLocation)</li>
	<li>GSM Operatorunden (3 Baz Istasyonundan Tahmini Lokasyon Bilgisi)</li>
	<li>GPS telefonlar yoluyla bulma</li>
	<li>HTML5 ile birlikte Lokasyonu browser'a sorma (GeoLocation)</li>
	<li>Fotoğrafın EXIF bilgisinden öğrenme</li>
</ul>
Yukarıdaki yöntemlerin hepsiyle konum bilgisini (longitude ve latitude) elde etmek mümkün.
Bunlardan GPS ve GSM ilgili olan yöntemler, makineden makineye ve operatorden operatore değişiklik gösterebileceği için bu yazının kapsamı dışındadır. GSM ve GPS üzerinden lokasyon çekmek özellikle lokasyonun güvenilirliği gerektiği durumlarda daha etkili olmaktadır. Tabii GSM ve GPS gibi sistemleri simule etmekte mümkün ama şimdilik, küçük bir kesimin yapabileceği bir iş.

<strong>Neler Yapılabilir?</strong>
<ul>
	<li><strong>Takip sistemleri; </strong> Kişi ya da aracın takibi için kullanılabilir.</li>
	<li><strong>En yakın lokasyon;</strong> Bulunduğunuz lokasyonun 10 kilometre çevresindekileri bulmak diyebilirim. (Birazdan bu konuda örnek bir uygulama yazacağız) Aklıma ilk gelen örnekler; eczaneler, lokantalar, tanıdık kimseler, ustalar ve kiralık evler  bulmak. Örnekler ve kullanım şekli hayal gücünüzle sınırlı görüldüğü üzere. Bunu bir iPhone yada Android uygulaması ile entregre edildiği düşünülürse tadından yenmez.</li>
	<li><strong>Lokasyona Göre Davranış;</strong>Sitenizin davranışları lokasyona göre değişiklik gösteriyor olabilir. Örneğin, bazı ürünleri sadece bazı lokasyonlar için satıyor olabilirsiniz. Koca bir listeyi müşterinizin karşısına çıkarmak pek anlamsız olabilir. Web 3.0'a hazırlandığımız şu günlerde siteler ne kadar akıllı olursa ve bizden ne kadar az içerik talep ederse o kadar iyi olacaktır.</li>
</ul>
<strong>Nasıl Yapılabilir?</strong>

<strong>IP'den lokasyon bulmak</strong> için, web üzerinde bu hizmeti alabileceğiniz çok fazla firma var. İlk aklıma gelenleri; <a href="http://www.ip2location.com/">IP2Location</a>, <a href="http://www.maxmind.com/">MaxMind</a>, <a href="http://www.geopostcodes.com/">GeoPostcodes</a>.

Bunların içinden ücretsiz bir sürümü bulunan MaxMind firmasının <a href="http://geolite.maxmind.com/">GeoLite</a> isimli ürünü ile ilk demomuzu gerçekleştireceğiz.

<strong>Gereksinimler</strong>
<ul>
	<li><a href="http://php.net">PHP 5</a></li>
	<li><a href="http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz">GeoLiteCity.dat</a></li>
	<li><a href="http://www.maxmind.com/app/php">PHP İçin GeoLocation API Modülü</a></li>
</ul>
Öncelikle ücretsiz şehir verisini indirelim.
<pre lang="bash"># Ornekte kullanilan GeoLiteCity.dat dosyasının kurulumu
su -
mkdir -p /opt/maxmind
cd /opt/maxmind
wget http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz
gunzip GeoLiteCity.dat.gz
chmod a+r -R /opt/maxmind

# PHP Modülünün kurulumu.
wget http://geolite.maxmind.com/download/geoip/api/php/geoipregionvars.php
wget http://geolite.maxmind.com/download/geoip/api/php/geoipcity.inc

# Eger Apache ayarlarınızda open_base_dir ayari aktif ise
# PHP kodunuzun bulundugu dizine koyun ve örnekteki yolu degistirin.
</pre>
Şimdi IP'den latitude ve longitude degerlerini bulan kodun demosunu yazalım.

<pre lang="php">
include("geoipcity.inc");
include("geoipregionvars.php");

$gi = geoip_open("/opt/maxmind/GeoLiteCity.dat", GEOIP_STANDARD);
$record = geoip_record_by_addr($gi, $_SERVER["REMOTE_ADDR"]);
geoip_close($gi);

echo "<h1>bulundugunuz sehir</h1><hr/>";
echo "<pre >".print_r($record, true)."</pre >";
</pre>

Bu demonun çalışan haline <a href="http://phparchitect.org/tr/demos/lokasyon-bazli-servisler-yaratmak/geolocation.php" target="demo">şuradan</a> erişebilirsiniz.

<p>
<strong>En yakın şeyi bulmak</strong> ile anlatılmak istenen bilinen bir lokasyonun etrafında bulunan (diyelim ki 1 kmlik) bir alan içerisindeki nesneleri bulmaktan söz edilmektedir. Örneğin bir ilan sitesi için bu kiralık veya satılık evler, araçlar ve çeşitli taşınır ve taşınmazlar olabilir. Ya da, "Ne/Nerede" servisi için, çilingir, taksi durağı ve eczanenin bulunduğu yerler de bulunabilir.

Bu konuda eğer web üzerinde araştırma yapmayı düşünüyorsanız, arama motorlarına "radius search" yazmanız yeterli olacaktır.  Karşınızda, lokasyon üzerine, özellikle <u>posta kodu (zipcode)</u> hizmeti sunan siteler çıkacaktır. Tahmin ettiğiniz üzere anahtar kelime, <strong>posta kodu</strong> bilgisi. Daha doğrusu mahalle seviyesine indirgenmiş longitude ve latitude değerlerine sahip olmak. Bu sayede, yarıçap hesabı <strong>(radius)</strong> yaparak, örneğin 1km'lik bir alana ait mahallelere erişemek mümkün. İşte işin büyüsü burada. <a href="http://yelp.com">Yelp</a> ve <a href="http://foursquare.com">FourSquare</a> bu şekilde size mekan bilgilerini verir.
</p>
<p>
Bu hesaplamanın nasıl yapıldığını araştırırken, <a href="http://codeguru.com">CodeGuru</a> sitesinde <a href="http://www.codeguru.com/Cpp/Cpp/algorithms/article.php/c5115/">Coğrafik Bölge Hesaplamaları</a> başlıklı bir makaleye rastladım. Kodlar C++ diliyle yazılmıştı. Bu işin mantığıyla ilgilenen <a href="http://www.fazlamesai.net/index.php?a=article&sid=3102">olay odaklı programcılar</a> için güzel bir makale. Ama yok hani PHP ile yazılmış kodları merak eden <a href="http://www.fazlamesai.net/index.php?a=article&sid=3102">ürün odaklı</a> programcı kardeşlerim için ise, Steven Brendtro tarafından PHP diline port edilen GeoCalc sınıfını ve <a href="http://imaginerc.com/software/GeoCalc/">şuradaki</a> makalesini tavsiye ederim.
</p>
<p>
Peki yarıçap hesabı yapmak için gerekli PHP kütüphanemizde var artık. Aşağıda anlatacağım örnek için, posta kodu veritabanı tablonuz olduğu varsayılmıştır. Yani şimdi bulmamız gereken, posta kodları seviyesinde latitude ve longitude değerleri. Bu konuda ücretli olmasına rağmen şiddetle tavsiye edebileceğim site  <a href="http://www.geopostcodes.com/index.php?pg=browse&grp=1&sort=1&niv=3&id=489&l=0">GeoPostcodes</a>. Gerçekten çok iyi bir içeriğe sahip. Diğer bir alternatif için ise, arama motorundan bulduğum ve hiç deneme fırsatı bulamadığım <a href="http://www.zip-codes.com/">ZipCodes</a> isimli site. Son olarak posta kodları ile ilgili ücretsiz siteler bulmanız mümkün ama bunların çoğu Amerika için geçerli :(
</p>

Peki şimdi gelin GeoCalc ile 1 km'lik bir alan nasıl bulduğumuzu inceleyelim.
<pre lang="php">
include_once("GeoCalc.class.php");
$oGC = new GeoCalc();

// IP'den lokasyon bulma yoluyla bulduğumuz değerler.
$dLongitude = -94.44590241;
$dLatitude = 38.7996;

// Ne kadarlık bir alanda sorgulama yapılacak?!
$dRadius = 1.00;  // in kilometers

// Yarıçap Hesabı.
$dAddLat = $oGC->getLatPerKm() * $dRadius;
$dAddLon = $oGC->getLonPerKmAtLat($dLatitude) * $dRadius;

// Sınırların belirlenmesi.
$dNorthBounds = $dLatitude + $dAddLat;
$dSouthBounds = $dLatitude - $dAddLat;
$dWestBounds = $dLongitude - $dAddLon;
$dEastBounds = $dLongitude + $dAddLon;

print "Merkezi Longitude: $dLongitude\n";
print "Merkezi Latitude: $dLatitude\n";
print "Yarıçap: $dRadius kilometre\n";

print "Kuzey Sınırı: $dNorthBounds\n";
print "Güney Sınırı: $dSouthBounds\n";
print "Doğu Sınırı: $dEastBounds\n";
print "Batı Sınırı: $dWestBounds\n";

// Örnek sql sorgusu ile hangi bölgeleri kapsadığı bulunur.
$strQuery = "SELECT * FROM PostalCodes " .
              "WHERE Latitude > $dSouthBounds " .
              "AND Latitude < $dNorthBounds " .
              "AND Longitude > $dWestBounds " .
              "AND Longitude < $dEastBounds";

</pre>

Bulunan bu bölge kodlarına bağlı kayıtların çekilmesi ve sayfada listelenmesiyle işlem tamamlanmış olur.

<p>
Son olarak, <strong>HTML5</strong> ile birlikte gelen lokasyon öğrenme yönteminden söz ederek yazımı sonlandırmak istiyorum. Bu yöntemin, IP'den lokasyon bulmaktan farkı web tarayıcınızdan izin ister ama bunun karşılığında tarayıcının makinede varsa GPS'ten ya da çeşitli servislerden öğreneceği kaliteli bir latitude ve longitude değeri sunar.
</p>
<pre lang="javascript">
if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(function(position) {
        result = "latitude:"+position.coords.latitude+"-";
        result += "longitude:"+position.coords.longitude;
        alert(result);
    });
} else {
    alert("Uzgunum, tarayicinizin cografik konum destegi henuz yok! HTML5 destegi olan bir tarayici kullanin.");
}
</pre>