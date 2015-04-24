---
layout: post
title: MacBook Üzerine Ubuntu 9.04 Kurulumu
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Uzun süredir Macbook almayı düşünüyordum. Bir arkadaşımın önerisiyle sahibinden.com sitesi üzerinden, bütçeme uygun bir "Macbook 3,1" satın aldım. Herşeyine yabancı olduğum PC dünyasından farklı ama ince düşünülmüş tasarımıyla çok güzel bir makine. Önerilerle birkaç yazılımı hemen yükledim. Ama geliştirme ortamı MAMP(macosx, apache, mysql ve php) kurulumu yaptım. Terminal üzerinde vim ile PHP kodları geliştiriyordum. Fakat, Turkish-Q klavyede @ işaretinin ALT+Q tuşu ile çıkıyor olmasından ve CMD+Q tuşununda uygulamayı sonlandırmak için ayarlanmasından dolayı kod yazarken biraz içerik kaybettim. (Belkide English-Q klavyeye geçmeliydim)

Virtualbox sanal makine uygulaması üzerine Ubuntu kurmama rağmen onunda kendi dertleri yok değildi. Macports ve Fink paket kurma uygulamalarıda aptitude ile kıyaslanamaz kötü ve yetersiz olduğunu söylemem gerek.

Projenizde sizin macbook'a alışmanızı bekleyemeyecek durumdaysa; "insanın sabır küpü" pek fazla dayanmıyor. Şuan size bu satırları Ubuntu üzerinden yazan biri olarak şunları söylemeliyim ki<strong>, </strong><span class="status-body"><span class="entry-content"><strong> <em></em></strong></span></span>

<span class="status-body"><span class="entry-content"><strong><em>"Macintosh'tan başka bilgisayar almam ama geliştirme ortamında ise Linux'tan şaşmam!"</em></strong></span></span>

Peki niyetim dual boot olarak MacOSX ve Ubuntu'yu birlikte çalıştırmaktı. Elimde ise tek bir partition vardı ve OSX kurmak içinde Leopard kurulum cd'si yoktu. Yani OSX'i silmeden ve partition yaratarak kurmam gerekiyordu. Araştırmalarım sonucunda Apple'ın BootCamp Assitant adında bir yazılımı olduğunu ve bunun partition'da yer açabileceğimi öğrendim. Ama bu yazılım MacOS 10.4 (Tiger) sürümü ile Mac üzerine kuruluyor. Leopard ile önce windows'a kurulan bir sürümü (v.2) olduğunu öğrendim. İndirdiğim tüm Bootcamp Assitant 2.0 uygulamalarında windows sürücüleri çıktı. Ubuntu'yu kurduğunuza wireless ethernet kartı tanımadığını gördüğünüzde çözümününde bu sürücülerden geleceğini bilmeniz yeterli.

Neyse bu kadar boş laf yeter. Bugün tek partitionlı Mac OS X Leopard olan bir işletim sistemine nasıl Ubuntu kurabildiğimi anlatacağım.
<ol>
	<li>İlk olarak MacOS'u güncelleyin. (Özellikle firmware paketini güncellemeniz önemli. Bu sayede rEFIt çalışabilir.)</li>
	<li>HFS+ dosya sistemi ile biçimlendirilmiş external bir harddiske ihtiyacınız var.</li>
	<li>Macbook diskini bölümlere ayırmak için BootCamp bulamadıysanız yapmanız gereken işletim sisteminin yedeğini harici bir diske kopyalayıp bu diskten bilgisayarı <a rel="nofollow" href="http://refit.sourceforge.net/" target="_blank">rEFIt</a> yardımıyla başlatmak. rEFIt MacOS'un dualboot için geliştirdiği EFI desteğini gayriresmi olarak ubuntu tarafından kopyalamıza yardımcı olur.</li>
	<li><a rel="nofollow" href="http://www.bombich.com/software/ccc.html" target="_blank">Carbon Copy Cloner</a> yazılımı yardımıyla tüm diskin bir başlatılabilir bir klonu alınır. Bu işlem diskinizin büyüklüğü ile orantılı olarak uzun sürer. :)</li>
	<li>Kopyalama işlemi tamamlanınca bilgisayar yeniden başlatıldığında rEFIt yazılımının menüsünün  yardımıyla harici diskten MacOS başlatılır.</li>
	<li>Finder içinden Applications / Utilities / Disk Utility uygulaması başlatılır. MacBook hard diski seçilir gelen formdan Partition sekmesine tıklanır ve bölümlendirme sırasıyla Windows için DOS dosya sistemi, Linux için DOS dosya sistemi ve geri kalan alan ise MacOS için HFS+ dosya sistemi ile biçimlendirilir. DOS dosya sistemleri sadece disk alanı açmak içindir. Sonra Windows için NTFS linux için ise ext ve swap alanları için yeniden bölümlendirileceklerdir.</li>
	<li>Carbon Copy Cloner yazılımı ile harici diskten macos için ayırdığınız bölüme geri kopyalayın.</li>
	<li>Ubuntu CD'si ile kurulumu yaparken dikkat etmeniz gereken, ubuntu için ayrılan alanda duran DOS dosya sistemini kaldırıp sırasıyla, linux dosya sistemlerini elle ayarlamanız gerektiğidir. Bootloader'ı MBR'a kesinlikle kurmamanız gerekir bu sebeple 100MB alanı /boot olarak mount edin. 2-3 gb alanı swap ve geri kalan alanıda ext4 (gerçekten hızlı) ile bölümlendirin. Kurulumdan bir önceki onay sayfasında Advanced menüsünden bootloader'ın MBR yerine yarattığınız sda2(/boot) alanına kurulumunu sağlamalısınız.</li>
	<li>Son olarak isterseniz, Windows kurulumu yapabilir ve BootCamp ile önerilen işlemleri yapabilirsiniz. Fakat ben bu kısıma girmeyeceğim.</li>
	<li>Sonra bilgisayarı yeniden başlatıyoruz ve görüyoruz ki rEFIt menüsünde MacOS ve Linux logoları bizi selamlıyor. Tebrikler kurulumu başarıyla tamamladınız. Ama işimiz henüz bitmedi. MacBook için küçük ayarlar yapmamız gerekiyor.</li>
	<li>Wireless ve diğer MacBook donanım ayarlarını aşağıdaki linklerde anlatıldığı şekilde yapabilirsiniz. <a href="https://help.ubuntu.com/community/MacBook3-1/Jaunty" target="_blank">https://help.ubuntu.com/community/MacBook3-1/Jaunty</a> <a href="http://www.isriya.com/node/1804/ubuntu-on-macbook-air" target="_blank">http://www.isriya.com/node/1804/ubuntu-on-macbook-air</a> Bu iki bağlantı size yol gösterecektir.</li>
	<li>Son olarak Turkish+Q klavyenizin ayarlarını yapmanız gerekiyor. Yanda { ", é, &lt;, &gt; } görebileceğiniz tuşlar, ubuntu üzerinde yanlış map edilmiştir. Bunu düzeltmenin yolu ise, xmodmap kullanmaktır.  Ev dizininizde .Xmodmap dosyası yaratın ve içine aşağıdaki satırları ekleyip yeniden başlattığınızda tuşların düzeldiğini göreceksiniz.</li>
</ol>
<blockquote><strong>~/.Xmodmap</strong>

keycode  94 = quotedbl eacute quotedbl eacute less degree<em></em>

<em>keycode  49 = less greater less greater bar brokenbar</em></blockquote>
<ol></ol>
İşte yapmanız gerekenler bundan ibaret. İşte çalışmak şimdi eğlenceli olmaya başladı :)
