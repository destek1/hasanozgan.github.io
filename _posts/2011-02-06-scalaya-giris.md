---
layout: post
title: Scala'ya Giriş
tags:
- akka
- Diğer
- lift
- programlama
- sbt
- scala
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Uzun zamandır Scala ile ilgili bir yazı dizisi yazma planım vardı. Yoğunluğum nedeniyle bugüne kısmetmiş ama bir miktar paslandığımı itiraf etmeliyim. Bu yıl daha çok ölçeklenebilirlik üzerine <a href="/2010/12/yeni-yilda-olceklenebilirlik-uzerine-planlar/">yazılar yazmak istediğimi dile getirmiştim</a>.

Ölçeklenebilirlik konulu yazılarımın aslına bakarsanız merkezinde <a href="http://scala-lang.org">scala programlama dili</a> olacak. İşin web bacağında lift web framework, dağınık haberleşme mimarilerinde (akka), ve dağınık veri tabanları konusunda (noSQL) özellikle MongoDB'den bolca konuşacağız.

Scala ile ilk kez tanışacaklar için Scala, ruby, java, c++ karışımı bir dil gibidir. Nasıl bir yazım biçimi olduğunu merak edenler için aşağıda bir hello-world programı yazdım.

{% highlight scala %}
object HelloWorld {
    def main(args: Array[String]) {
        println("Hello, world!")
    }
}
{% endhighlight %}

Bu yazım biçimi bana yetmez diyenler <a href="http://www.scala-lang.org/node/166">şu adresten</a> daha fazla kod örneği bulabilirler.

Scala'nın özelliklerine hızlıca bir bakacak olursak;
<ul>
	<li>Hem bir betik (script) dili, hem de derlenebilme özelliği olan bir dildir.</li>
	<li>Scala derleyicileri kaynak kodunuzu, Java ve/veya <a href="http://hestia.typepad.com/flatlander/2009/01/getting-started-with-scala-on-net.html">.NET</a> mimarilerine göre derlenebilir.</li>
	<li>Dil, özellikle ölçeklenebilirlik alanına yönelik güçlü bir dildir.</li>
	<li>Scala diliyle yazdığınız kodları deneyebilmeniz için CLI özelliğide bulunmaktadır.</li>
</ul>
Scala diliyle ilgili türkçe bir kitap hazırlığı içindeyim. Ücretsiz dağıtmayı düşündüğüm bu kitaba <a href="/belgeler/scala-rehberi">adresinden</a> ulaşabileceksiniz.

### Geliştirme Ortamı ###
Scala derleyicileri, kodları derlediğinde JVM mimarisine dönüştüğü için Java araçlarıyla tam uyumludur. Java'daki birçok teknolojiyi kullanabilirsiniz.

Scala'nın bir CLI(command-line interpreter) arayüzü olduğunu söylemiştim. gelin hızlıca Scala ile birşeyler yazalım.
{% highlight bash %}
$ scala
This is an interpreter for Scala.
Type in expressions to have them evaluated.
Type :help for more information.

scala> 

# Example 1
scala> 1 + 2
unnamed0: Int = 3

# Example 2
scala> unnamed0 * 3
unnamed1: Int = 9

# Example 3
scala> println("Hello, world!")
Hello, world!
unnamed2: Unit = ()
{% endhighlight %}

Scala'ya daha fazla giriş yapmak için :) artima sitesindeki <a href="http://www.artima.com/scalazine/articles/steps.html">First Step to Scala</a> yazısını tavsiye ederim.

Scala'yı popüler programlama editörleri <a href="https://lampsvn.epfl.ch/trac/scala/browser/scala-tool-support/trunk/src/vim">Vim</a> ve <a href="https://lampsvn.epfl.ch/trac/scala/browser/scala-tool-support/trunk/src/emacs">Emacs</a> ile yazabileceğiniz gibi, popüler Java IDEleri (<a href="http://wiki.netbeans.org/Scala">Netbeans</a>, <a href="http://scala-ide.org">Eclipse</a>, I<a href="http://plugins.intellij.net/plugin/?id=1347">ntellij IDEA CE</a>) ile yazabilirsiniz. Ben tercihimi Eclipse'ten yana kullandığımı ama Intellij'nin eklentisinin gerçekten başarılı olduğunuda belirtmeliyim. Maalesef Netbeans nasıl hiçbir fikrim yok ama Lift Framework'un yaratıcısı Netbeans'ı kullandığına dair 1-2 yazıya rastlamıştım. Kısacası burada karar size kalıyor.

### Java ile Scala Arasındaki Farklar ###
Java ile Scala arasındaki farkları <a href="http://blogs.sun.com/sundararajan/entry/scala_for_java_programmers">şuradaki yazıda </a>bulabilirsiniz. Ayrıca hemen aşağıda bu konuda bulduğumu sunumuda inceleyebilirsiniz.

<iframe src="//www.slideshare.net/slideshow/embed_code/key/HyLbK8DxgzLfN2" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/davetron5000/scala-for-java-developers-intro" title="Scala for Java Developers - Intro" target="_blank">Scala for Java Developers - Intro</a> </strong> from <strong><a href="//www.slideshare.net/davetron5000" target="_blank">David Copeland</a></strong> </div>

<br/>
### Scala Araçları (birkaç iyi oyuncak) ###
### SBT (Simple Build Tool) ###
Scala ile Java teknolojilerinin tümünden faydalanabileceğinizden yukarıda söz etmiştim. Scala programcıları ilk zamanlar Maven kullansalarda, sonraları <a href="http://code.google.com/p/simple-build-tool">Simple Build Tool</a> (aka SBT) isimli çok tatlı bir yapılandırma aracı kullanılmaya başlandı. Bu araçla yapılandırma işlemlerinizi, Scala diliyle yapabiliyorsunuz. Arkada, ivy ve maven kullanan bu başarılı araç için aynı maven'da olduğu gibi hızlıca eklentilerde yazabiliyorsunuz.

Örneğin ben proje kodumu sbt ile build edecek şekilde hazırlayıp. Buradan da <a href="https://github.com/musk/SbtEclipsify">Eclipsify</a> isimli SBT eklentisi ile eclipse projesini yaratıyorum. Ayrıca SBT'yi, Eclipse içinden kullanmak <a href="https://github.com/frank06/sbt-eclipse-plugin">şuradan</a> ekletiye ulaşabilirsiniz.

### Scalatra Web Framework ###
<a href="https://github.com/scalatra/scalatra#readme">Scalatra</a> eskiden Step olarak anılan ve Ruby Sinatraya benzeyen bir web çatısı. Küçük projeler için hızlı uygulama yazmayı amaçlayanlar için iş görebilir. Ama daha çok fazla yolu olduğunu eklemekte fayda var. Aşağıda adından söz edeceğim Lift framework'e kıyasla çok eksiği bulunuyor.

### Lift Web Framework ###
<a href="http://blog.lostlake.org/">David Pollak</a> (a.k.a <a href="http://twitter.com/dpp">@dpp</a>) tarafından yazılan web çatısıdır. David, framework'u hazırlarken birçok frameworkü incelemiş ve uygun gördüğü özelliklerini <a href="http://liftweb.net">Lift Web Framework</a>'e dahil etmiştir. Bugün en büyük referansı Foursquare olarak verilebilir. Yeni versiyonlarla MVC patterni kullanılarak web projeleri yazılabilse de aslında bileşen (Snippet) mimarisine dayanır. Kendi içinde ORM gibi birçok alt proje bulunduğunu iletmekte yarar var. 

Lift <a href="http://seventhings.liftweb.net/">"Seven Thins"</a> isimli sayfasına girerek diğer frameworklere kıyasla yarattığı farkların neler olduğunu görebilirsiniz.

<a href="http://liftweb.net">Lift Framework</a>'ün belgelemesi gerçekten iyidir. Biri David Pollak tarafından olmak üzere iki özgür kitap projesi bulunmaktadır. Bunlar;

<ul>
	<li><a href="http://simply.liftweb.net/">Simply Lift</a></li>
	<li><a href="http://exploring.liftweb.net/">Exploring Lift</a></li>
</ul>

Lift projesinin kaynak kodlarına ve örnek uygulamalarına <a href="http://github.com/lift">Github üzerinde bulunan adresinden</a> erişebilirsiniz.

Scala dili ile ilgili başlangıç sorularınıza umarım cevaplar verebilmişimdir. Scala gerçekten eğlenceli ama bir o kadarda detaylı bir dil. Oracle'ın Sun'ı satın aldıktan sonra yapacakları belirsizliğini korurken bu konuda bir B planı olması bence gerçekten çok rahatlatıcı. Eğer sizde Scala ile birşeyler yapmayı düşünüyor ve kendinizi yalnız hissediyorsanız, <a href="http://scala-tr.org">Scala Türkiye</a> ekibine katılabilirsiniz. Topluluk bu konuda etkinlikler yaparak faliyetlerine çok kısa bir süre içerisinde başlayacaktır.

Bir sonraki yazımızda elinizi Scala'ya bulamaya hazır olun. Scala diliyle framework kullanmadan Web dünyasına giriş yapacağız. 
<br/>
