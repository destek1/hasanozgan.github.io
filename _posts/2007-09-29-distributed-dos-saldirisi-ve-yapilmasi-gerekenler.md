---
layout: post
title: Distributed DoS Saldırısı ve Yapılması Gerekenler!
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
<p style="padding-left:10px;"></p>

İnternetin bir yıl içinde büyüyen ve yenilikçi fikriyle dikkatleri üzerine çeken bir şirketi (adını vermeyeceğim) bir haftadır ara-ara <a href="http://sozluk.sourtimes.org/show.asp?t=ddos">d-DoS</a> saldırılarına maruz kalıyordu. Dün çok ciddi bir saldırı oldu. (saniyede 16.000 connection), ISP'nin bant genişliğinin dahi kaldıramadığı bu saldırıyı engellemek için tüm gün TCP paketlerini inceleyerek ve kafamızı duvardan duvara vurarken, saldırının sahibine yaratıcı küfürler bularak geçirdik. Ve nihayet en sonunda saldırıyı engelleyebildik. Nasıl engellediğimiz ile ilgili bilgiye aşağıda bulabilirsiniz.<strong></strong>

<strong>1)</strong> Önce atağın hangi sayfaya geldiğini tespit edin!. Ve tespit ettikten sonra o sayfayı IPS üzerinden bloklayın.

<strong>2)</strong> Eğer saldırı bir sayfa değilde bir URL'e geliyorsa, ozaman çok basit bir index.html sayfası hazırlayıp, o sayfadan ana sayfanıza javascript redirect yapın. Basit index.html sayfasının önemi şundan kaynaklanıyor. DoS saldırılarını Load Balancer'lar zaten yönetebiliyorlar. Fakat bunu yapmak için yapılan isteğin tamamlanmış olması gerekiyor. Eğer 24 saniyede yüklenen bir sayfanız varsa, load balancer faydadan daha çok zarar getiriyor. Hatta benim önerim, index.html sayfanızın dinamik bir şekilde bir açılış sayfası adresine yönlendirme yapması.

<strong>3)</strong> Bu sırada gelen paketleri inceleyin. Genelde DoS saldırıları küçük programlar vasıtasıyla yapılır ve bu küçük programların kullandığı HTTP kütüphaneleri header'in User-Agent: alanina kendilerini yazarlar. Buradan tanınan paketler yakalanabilir. Yada kendi requestleriniz ozel bir header bilgisi ile gönderilebilir. vs..

<strong>4)</strong> Kişinin IP-Spoofing yapıp yapmadığını IP'lerin görünen uzaklığı ve TCL bilgisinden yakalamaya çalıştık. Gördük ki farklı makinelerden zombi requestler açılıyor..
