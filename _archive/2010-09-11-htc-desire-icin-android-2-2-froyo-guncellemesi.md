---
layout: post
title: HTC Desire için Android 2.2 (Froyo) Güncellemesi
tags:
- android
- clockworkmod
- Diğer
- froyo
- goldcard
- htc desire
- htc sense
- reflash
- unrevoked
- update.zip
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  _wp_old_slug: ''
---
iPhone'nun kendince koyduğu saçma kurallardan gerçekten o kadar bunaldım ki, yaklaşık 3-4 ay önce HTC Desire satın aldım. Android birçok yönden gerçekten de özgür bir platform ve mobil yaşam sunuyor. Android 2.2 sürümü ile beraber özgürlük başka bir boyut kazandı. Peki, Android 2.2 neler <a href="http://developer.android.com/sdk/android-2.2-highlights.html">getiriyor</a>;
<ul>
	<li>Flash 10.1 desteği</li>
	<li>Portable Wi-fi hotspot.</li>
	<li>Çok dilli klavye</li>
	<li>Performans iyileştirmeleri (JiT Compiler, Kernel vb..)</li>
	<li>Google uygulamalarının güncellemeleri</li>
	<li>Radyo güncellemesi</li>
	<li>Yeni Android geliştirici özellikleri (push sync, hata bildirimi gibi)</li>
	<li>Exchange desteği</li>
	<li>Kamera ve galeri ile ilgili değişiklikler</li>
	<li>Daha uzun batarya ömrü.</li>
</ul>
Yukarıda sayılan özellikler gerçekten iştah açıcı. Bu sebeple lafı çok uzatmadan, HTC Sense arabirimini koruyarak güncelleme yapabileceğinizi anlatacağım.

<em><strong>Aşağıda anlatılan işlem sırasında telefonunuza birşey olursa tüm sorumluluk size aittir!</strong></em>

<em>Peki şimdi işe başlayalım;</em>
<ul>
	<li>Öncelikle yedeklerinizi alın, çünkü tüm bilgileriniz SİLİNECEK!.. (Yedeklerinizi almak için HTC Sync ya da Google Sync kullanabilirsiniz)</li>
	<li>Yedeklerinizi aldıktan sonra ilk yapmamız gereken, Recovery moda geçmek için, Mikro SD kartımızı <strong>Goldcard</strong> denilen bir biçime çevirmek.
<ul>
	<li>Android SDK'yı <a href="http://developer.android.com/sdk/index.html">şuradan</a> indirip, kurmanız yeterli.</li>
	<li>Micro SD kartınızın takılı olduğu Desire’ınızı bilgisayarınıza bağlayın ve Settings/Applications/Development/USB Debugging Mode‘u aktif olarak işaretleyin.</li>
	<li>Komut satırına geçtiğinizde, /tools dizininde adb isimli bir uygulama göreceksiniz. Öncelikle, "adb devices" komutu ile cihazın seri numarasını kontrol edin. Eğer bunu görmüyorsanız birşeyler yanlış demektir.</li>
	<li>”adb shell cat /sys/class/mmc_host/mmc1/mmc1:*/cid“ komutunu çalıştırın. Karşınıza şunun gibi (022600bd227d9c0447322407092d5324) uzun bir numara çıkacak.</li>
	<li><a href="http://hexrev.soaa.me/">http://hexrev.soaa.me/</a> adresine gidin ve bu uzun kodu tersine çevirin.</li>
	<li><a href="http://psas.revskills.de/?q=goldcard">http://psas.revskills.de/?q=goldcard</a> adresine giderek tersine çevirdiğiniz numarayı ve kendi geçerli e-mailinizi girerek goldcard.img dosyasını edinin. Dosya e-mail adresinize gelecek.</li>
	<li>Şimdi image dosyamızı MikroSD kartımıza yazmamız gerekiyor.
<ul>
	<li><strong>Mac OS X ya da Linux kullanıyorsanız;</strong></li>
	<li>Komut satırına geçin.</li>
	<li><strong>"diskutil list" </strong>komutu ile HTC Desire telefonunuzdaki SD kartı görüp görmediğinizi kontrol edin. DOS_FAT_32 olarak tanımlı olan kısmı kullanacaksınız. Diyelim ki örneğimizde bu /dev/disk2 olsun.</li>
	<li>Daha sonra SD kartınızı unmount edin. Bunun için <strong>"diskutil unmountDisk /dev/disk2"</strong> komutunu çalıştırabilirsiniz.</li>
	<li>Şimdi goldcard'ımızı oluşturalım. Bunun için <strong>"sudo dd bs=512 if=~/goldcard.img of=/dev/disk2"</strong> komutunu çalıştırmamız yeterli. Unutmayın disk2 sizde farklı bir numaraya sahip olabilir.</li>
</ul>
<ul>
	<li><strong>Windows kullanıyorsanız;</strong></li>
	<li>HxD isimli Hex editörü indirin, <a href="http://download.cnet.com/3001-20_4-10891068.html?spi=de6596f3025d2a1f103d2e6f7728b7be">bu linkten indirebilirsiniz</a>.</li>
	<li>HxD yi bilgisayarınıza kurun ve çalıştırın. Windows Vista ya da 7 kullanıyorsanız “Yönetici Olarak Çalıştır” ile açın.</li>
	<li>“Extra” sekmesinden “Open Disk” i seçin. “Physical Disk” (burası önemli, mutlaka physical olmalı) seçeneği altından, “Removable Disk” i seçin ve “Open as ReadOnly” seçeneğindeki işareti KALDIRIN ve OK e basın.</li>
	<li>Tekrar “Extra” menüsüne gelin ve “Open Disk Image” i seçin. Size e-mail ile gelen goldcard.img dosyasını seçin ve açın. Şimdi iki farklı sekme görmeniz gerekli, biri “Removable Disk” ya da SD kart, diğeri ise “goldcard.img” olmalı. “Sector Size” 512 (Hard disks/Floppy disks) şeklinde uyarı aldığınızda OK‘e basın.</li>
	<li>“goldcard.img” sekmesine tıklayın, “Edit” menüsünden “Select All” deyin ve yine Edit menüsünden “Copy” deyin.</li>
	<li>“Removable disk” sekmesine tıklayın. Sıfırıncı satırdan 170 inci satıra kadar (170 de dahil) seçin ve Edit menüsünden “Paste Write” seçeneğine tıklayın.</li>
	<li>“File” menüsünden “Save” e tıklayın ve editörü kapatın. Artık goldcardınız hazır.</li>
</ul>
</li>
	<li> Goldcard'ı hazırladıktan sonra <a href="http://www.megaupload.com/?d=WUPI07UO">HTC Sense ve Froyo 2.2'yi içeren güncelleme (ROM) dosyası</a>nı ve <a href="http://android.adamg.co.uk/bravo/radio/32.43.00.32U_5.09.00.20.zip">radio uygulaması için gerekli olan dosyayı</a> indirmeniz gerekmektedir. Her iki dosyayı MikroSD karta kopyaladıktan sonra <em><strong>Official_FroYo_Market_fixed.zip</strong></em> isimli dosyayı <em><strong>update.zip</strong></em> olarak değiştirmelisiniz!.</li>
	<li>Şimdi yapmamız gereken <em>reflash</em> işlemi için telefonumuzu <em>ClockworkMod</em>'a geçirmek.
HTC ürünleri için tüm platformlarda çalışan ve Clockworkmod'a geçişi sağlayan bir <a href="http://unrevoked.com/">unrevoked</a> adında bir uygulama mevcut. Bu uygulamayı kullanarak telefonu clockworkmod'a çevirmek mümkün. Uygulamalı olarak çevirme işlemini nasıl olacağını <a href="http://www.youtube.com/watch?v=KkaQe-uim5k&amp;feature=player_embedded#!">youtube da bulunan video</a>da izleyebilirsiniz.

Clockworkmod'a geçiş yaptıktan sonra yukleme işlemini tamamlamanızla birlikte işlem tamamlanmış olacaktır.</li>
</ul>
</li>
</ul>

Eğer clockworkmod'da iken sorunsuz bir şekilde kurulum işlemini yaptıysanız, telefonunuz yeniden başladığında Android 2.2 versiyonu ile başlayacak. İşte hepsi bu kadar. Froyo'nun güzellikleri şimdiden hayırlı olsun.

<strong>Kaynaklar:</strong>
<a href="http://theunlockr.com/2010/06/07/how-to-root-the-htc-desire/">http://theunlockr.com/2010/06/07/how-to-root-the-htc-desire/</a>
<a href="http://theunlockr.com/2010/03/10/how-to-create-a-goldcard/">http://theunlockr.com/2010/03/10/how-to-create-a-goldcard/</a>
<a href="http://developer.android.com/sdk/index.html">http://developer.android.com/sdk/index.html</a>
<a href="http://www.knowyourcell.com/htc/htc-desire/desire-guides/474135/how_to_root_the_htc_desire.html">http://www.knowyourcell.com/htc/htc-desire/desire-guides/474135/how_to_root_the_htc_desire.html</a>
<a href="https://www.andronova.net/android-teknik-bilgi/htc-desire-icin-root-clockworkmod-recovery-dj-droid-v10-h4228.html">https://www.andronova.net/android-teknik-bilgi/htc-desire-icin-root-clockworkmod-recovery-dj-droid-v10-h4228.html</a>
<a href="http://wiki.cyanogenmod.com/index.php?title=Full_Update_Guide_-_HTC_Desire">http://wiki.cyanogenmod.com/index.php?title=Full_Update_Guide_-_HTC_Desire</a>
<a href="http://www.dkszone.net/unrevoked-root-htc-android-phones-evo-4gdesiredroid-incredible">http://www.dkszone.net/unrevoked-root-htc-android-phones-evo-4gdesiredroid-incredible</a>
<a href="http://www.koushikdutta.com/2010/02/clockwork-recovery-image.html">http://www.koushikdutta.com/2010/02/clockwork-recovery-image.html</a>
