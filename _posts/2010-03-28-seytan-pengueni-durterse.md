---
layout: post
title: Şeytan, Pengueni Dürterse
tags:
- ! '*nix'
- cron
- daemon
- Diğer
- linux
- pear
- php
- system
- unix
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
<p>Günümüzde birçok site arkada yapılacak görevleri çalıştırmak için görev yöneticileri kullanılır. Crontab (Zaman ayarlı) ve Daemon (kendi halinde çalışan) iki görev yöneticinin arasındaki bence tek fark (durum bu kadar basit olmasada) Crontab'ın 1 dakikanın altındaki süreçlere göre çalışmamasıdır. Bu görevler için Daemon denilen ve <strong>/etc/init.d</strong> altında tetiklenen ve sinyallerle çalıştırılıp durdurulabilen ve process id değeri üreten bir teknolojiye ihtiyaç duymasıdır. Daemon'lar init.d altında bir çalıştırıcı scripte sahip olmaya bilir ama durdumak istendiğinde güç kullanılarak öldürülmesi (kill)  gerekir ki, kritik işlerde bu pek tehlikeli bir yöntemdir. Init.d altındaki başlatma scripti bir proses(PID) dosya yaratır ve daemon'u çalıştırır. Sonrasında durdumak isterse daemon'a sinyal gönderir. Böylece uygulama durma sinyalini görünce düzgün bir şekilde sonlanır. Crontab ise belli bir işin bellir bir saatte yapılmasını sağlar. Saatte bir, her 15 dk.'da bir ayın 5. günü, her çarşamba saat 15'te gibi...</p>
<!--more-->
<p>Kullanım alanlarına birkaç örnek vermek gerekirse; </p>
<p> <strong>Daemon</strong>;  Özellikle kuyruktaki işleri işlemek için çok kullanılır.</p>
<ul>
	<li>Video converter</li>
	<li>Email/SMS gönderme</li>
	<li>RSS ayrıştırma.</li>
</ul>
<strong>Cron;</strong>
<ul>
	<li>Günde bir kez gönderilecek işler. Örneğin; doğum günü epostaları.</li>
	<li>Ayda hatta yılda bir kez yapılacak işler. Anneler gününde temanın otomatik olarak değiştirilmesi.</li>
	<li>Haftanın belli bir günü yapılacak olan işler. Her Pazartesi indirim puanı oluşturup, rastgele 500 üyeye gönderme.</li>
	<li>Saatte bir yapılacak işler, Site için RSS oluşturma.</li>
</ul>
Daemon yazmak genelde C dili ile yazılan işlerdendir. Çünkü bu iş hem performans hem de sistem programlama(sinyaller ve prosesler) bilgisi  gerekir. Buna rağmen, işin mantığı ise  PHP, ve benzeri web dillerinde yazılmıştır. Belki de biraz bu sebeplerle Crontab ile görev tanımı yapılır. Crontab kullanmak güzeldir ama kurulum sürecinde ek yük getirir. Bunların doğru bir şekilde çalıştığının kaydının tutulması (<strong>loging</strong>) ve gözlenmesi (<strong>monitoring</strong>) işlerinin yapılmasıda cabası.

<p> Bu yazı <a title="Chronical Task Management Tool" href="http://code.google.com/p/chronical/" target="_blank"><strong>Chronical</strong></a> projesinin bilgi tasarımının ilk taslaklarını içermesinin yanında aktif olan mevcut uygulamalardan örnekler de verilecektir.</p>

<p><i><strong>Peki bu işleri ne şekilde yapımak gerekir?</strong></i></p>
<p><strong>1) System_Daemon PEAR Paketi</strong></p>
<p> <a href="http://pear.php.net/" target="_blank">PEAR</a> kütüphanesi içerisinde bulunan ve <a href="http://kevin.vanzonneveld.net/">Kevin van Zonneveld</a> tarafından geliştirilen <a href="http://pear.php.net/package/System_Daemon" target="_blank">System_Daemon</a> paketi kolayca linux daemonları yaratmanıza olanak verecek olan harika bir araçtır. Becerileri;
<ol>
	<li>İşletim sistemine özel başlangıç ayarlarının ve kurulumlarının kolayca yapılabilmesi.</li>
	<li>İşlem kaydı (loging) tutalbilmesi. Ve PEAR kütüphanesi ile uyumluluk</li>
	<li>Kullanım kolaylığı, birazdan örnek uygulamada da görebileceksiniz</li>
	<li>Sinyallerle çalışma ve özelleştirme</li>
</ol>
<strong>System Daemon Kurulum;</strong>

Linux sunucunuzda PEAR kurulu ise şu şekilde;
<pre lang="bash">$ pear install -f System_Daemon
</pre>
Yada <a href="http://download.pear.php.net/package/System_Daemon-0.10.2.tgz" target="pear">şuradan</a> indirerek kullanabilirsiniz.

<strong>Kullanım;</strong>

<strong>job/sms_sender.php</strong> isimli bir php dosyası yaratalım.
<pre lang="php">// Gerekli olan Daemon kütüphanesi.
// Bu kütüphane include_dir dizininin gösterdiği bir yerde olmalı.
require_once "System/Daemon.php";

// İzin verilen parametreler
$runmode = Array (
    // tek başına çalışması için
    'standalone' => false,
    // initd dizininde çalıştırma betiği yaratır.
    'write-initd' => false,
);

// Scan command line attributes for allowed arguments
foreach ($argv as $k=&gt;$arg) {
    if (substr($arg, 0, 2) == '--' && isset($runmode[substr($arg, 2)])) {
        $runmode[substr($arg, 2)] = true;
    }
}

// appName minimum gerekli olan parametredir.
System_Daemon::setOption("appName", "sms_sender");

// System_Daemon::setOption ile tek tek  ya da
// System_Daemon::setOptions($options) ile toplu olarak girilebilir.

$options = array(
    //'appName' => 'sms_sender',
    'appDir' => dirname(__FILE__),
    'appDescription' => 'MT SMS Sender',
    'authorName' => 'Hasan Ozgan',
    'authorEmail' => 'hasan@ozgan.net',
    'sysMaxExecutionTime' => '0',
    'sysMaxInputTime' => '0',
    'sysMemoryLimit' => '1024M',
    'appRunAsGID' => 1000,
    'appRunAsUID' => 1000,
);
System_Daemon::setOptions($options);

// Eger daemon olarak çalışmayacaksa
// System_Daemon::start() methodu ile başlatılabilir.
if ($runmode["standalone"]) {
    System_Daemon::start();
}

// job --write-initd parametresi ile çalıştırıldığında kendini kaydeder.
// açılışta çalıştırıldığında ise --init.d parametresi alır.
if (!$runmode["write-initd"]) {
     System_Daemon::info('not writing an init.d script this time');
} else {
    if (($initd_location = System_Daemon::writeAutoRun()) === false) {
        System_Daemon::notice('unable to write init.d script');
    } else {
        // parametreli log örneği...
        System_Daemon::info(
            'sucessfully written startup script: %s',
            $initd_location
        );
    }
}

// Daemon stop sinyali gelene kadar çalışmaya devam eder.
while (!System_Daemon::isDying()) {
   // Buraya işinizle ilgili kodları eklemelisiniz.

   $messages = OutgoingSMS::fetchMessages();
   foreach ($messages as $message) {
       if (!$message->send()) {
            System_Daemon::error("Message not send");
       }
   }

   // Daemonlarda önemli olan sonsuz döngüde bir miktar
   // işlem yapıp sistemi dinlendirmek gerekir.
   // Bunun için ise iterate methodu ile saniye cinsinden
   // bir süre vererek çağrı yapmak gerekir.
   System_Daemon::iterate(5);
}

System_Daemon::stop();
</pre>

<p>
Yazdığımız scripti tek başına çalıştırmak için ise;
<pre lang="bash">
$ job/send_sms --standalone
</pre>
yazmamız yeterlidir. Service birkez çalışıp sonlanacaktır.
</p>

<p>
Servisimizi init.d altına kaydetmek için ise;
<pre lang="bash">
$ sudo job/send_sms --write-initd
</pre>
yazmamız yeterlidir. Eğer burada hata alırsanız, init.d dizinin yazma haklarını kontrol etmeniz gerekir.
<pre lang="bash">
$ sudo chmod a+w /etc/init.d
</pre>
</p>

Bu işlemleri yaptıktan sonra <strong>appName</strong> parametresinde girdiğimiz isme göre;
<ul>
<li>/etc/init.d/send_sms</li>
<li>/var/log/send_sms.log</li>
<li>/var/run/send_sms/send_sms.pid</li>
</ul>
dosyaları oluşturulur.
İşletim sisteminin açılışta servisi çalıştırması için kayıt etmek gerekir.
<pre lang="bash">
# kayıt için
$ sudo update-rc.d send_sms defaults
# kaldırmak için ise
$ sudo update-rc.d -f send_sms remove
</pre>

<p><strong>2) Periodic Kütüphanesi</strong></p>
<p><strong>Arbit</strong> firması tarafından geliştirilen <a href="http://arbitracker.org/periodic.html">Periodic</a> kütüphanesini kullanabilirsiniz. Bu kütüphane crontab işlerini kendi sarmalayan biraz daha karmaşık bir mimariye sahiptir.
</p>
<pre lang="xml">
<?xml version="1.0"?>
 <task>
  <config>
     <reScheduleTime>92384032</reScheduleTime>
     <timeout>92384032</timeout>
  </config>
  <command type="shell">
     <!-- ... -->
  </command>
  <command type="vcsWrapperUpdate">
     <!-- ... -->
  </command>
  <!-- ... -->
</task>
</pre>
<p>
Periodic ile ilgili daha detaylı bilgiyi <a href="http://arbitracker.org/periodic/design.html">şuradan</a> alabilirsiniz.
</p>
<p><strong>3) Chronical Job Management Projesi</strong</p>
<p>
Bu proje benim yapacağım hem cron hem de daemon desteği ile melez çalışacak bir projedir. Henüz fikir halindedir. Projene adresine <a href="http://chronical.googlecode.com">şuradan</a> ulaşılabilir.
</p>
<p>
Bu proje servis işlerinizi hızlı ve kolay bir şekilde merkezi bir yerden yönetmeniz, durumunu kontrol etmenizi amaçlar.
</p>
<p><strong>Özellikleri</strong>
<ul>
   <li>Yaml ile kolayca güncellenebilen ayar dosyası</li>
   <li>Daemon kaydetme, kaldırmak ve durum bilgisi almak için kullanılacak çalıştırılabilir betik</li>
   <li>İş mantığınızı barındıran kodları çalıştıracak Abstract sınıf.</li>
</li>
</ul>
</p>
<p>
<strong>Örnek proje ayar dosyası (task.config);</strong>
<pre lang="yaml">
# Period Format
# second minute hour day month dayOfWeek weekOfMonth
# second: 0-59
# minute: 0-59
# hour: 0-23
# day: 1-31
# month: 1-12
# dayOfWeek: 1-7
# weekOfMonth: 1-5

# proje adina göre tek bir daemon oluşur.
# Bu daemon işlerin tamamını alt prosesler yaratarak yönetir.

proje_adi:
    gorev_adi:
        class: Application_Jobs_SmsSender
        # her 30 saniyede bir çalış anlamında.
        period: */30 * * * * *
    change_theme:
        class: Application_Jobs_ChangeTheme
        # Mayıs ayının ikinci pazar günü saat gece 2'de
        # Anneler gününde çalış.
        period: * 2 * 5 7 2
</pre>
</p>
<p><strong>Arayüz Sınıfı</strong></p>
<pre lang="php">
interface Chronical_Job_Interface
{
     // Ayar dosyasına verilen sınıfların bu
     // arayüzden gerçekleştirilmesi gerekir.
     public function run();
}
</pre>

<p><strong>Örnek Sınıfı</strong></p>
<pre lang="php">
class Application_Jobs_SendSms
                    extends Joy_Application
                    implements Chronical_Job_Interface
{
     public function run()
     {
           // TODO: Yapılacak işler....
     }
}
</pre>

<p><strong>Örnek log ayar dosyası;</strong> Bu dosya chronical uygulamasının log ve pid ayarları ile ilgili bir dosyadır.  Ubuntu ve debian temelli dağıtımlar için <strong>/etc/chronical.ini</strong>
</p>
<pre lang="ini">
[folders]
     folder.log = /var/log/
     fodler.pid = /var/run/
     folder.init.d = /etc/init.d
[defaults]
; seconds
     default.sleep_time = 5
</pre>
<p><strong>Düşünülen betik dosyası örnek işler</strong></p>
<pre lang="bash">
# OS startup install for init.d
$ chronical install task.config

# OS startup uninstall for init.d
$ chronical uninstall task.config

# Görev çalıştırma
$ chronical start proje_adi:gorev_adi

# Görev durdurma
$ chronical start proje_adi:gorev_adi

# Görev durumunu görme
$ chronical status proje_adi:gorev_adi
</pre>

Kısaca Unix sistemleri üzerinde daemon ve crontab işleri bu şekilde. (:
