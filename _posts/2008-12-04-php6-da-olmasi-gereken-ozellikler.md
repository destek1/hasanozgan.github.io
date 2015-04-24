---
layout: post
title: PHP 6'da Olması Gereken Özellikler
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Hayalini kurduğum framework için çıktığım yolda hergün yeni şeyler öğreniyorum. İtiraf etmem gerekiyorki ASP.NET mimarisinden çok etkilendim. Yazılım mimarileri ile uğraştığımdan dolayı sanırım C# diline ayrı bir sempatim var. Her açıdan çok iyi tasarlanmış bir dil. PHP'de web için biçilmiş kaftan fakat nesne yönelimli mimariler geliştirirken çok eksik olduğunu görüyoruz. Neden C# değilde PHP yazdığım sorusu aklınıza gelebilir. Bunun en büyük sebebi, C# projesinin Windows gibi baş ağrıtan kötü bir işletim sistemi üzerinde koşması geliyor. Mono ile daha önce bir web projesi geliştirmiş biri olarak yetersiz olduğunu söyleyebilirim.

Bu yazıda PHP6'da olması gerektiğini düşündüğüm özelliklerden söz edeceğim. Öncesinde küçük bir araştırma yaptım. Benim gibi PHP6 beklentileri olanlar var mı diye? <a href="http://www.stubbles.org/authors/1-Stephan-Schmidt">Stephan Schmidt</a>'in 6 parçadan oluşan <a href="http://www.stubbles.org/archives/5-My-wishlist-for-PHP-6,-pt1-The-object-type-hint.html">y</a><a href="http://www.stubbles.org/archives/7-My-wishlist-for-PHP-6,-pt2-Namespaces.html">a</a><a href="http://www.stubbles.org/archives/8-My-wishlist-for-PHP-6,-pt3-Annotations.html">z</a><a href="http://www.stubbles.org/archives/15-My-wishlist-for-PHP6,-pt4-static-initializers.html">ı</a><a href="http://www.stubbles.org/archives/19-My-wishlist-for-PHP6,-pt5-extphar.html">s</a><a href="http://www.stubbles.org/archives/24-My-wishlist-for-PHP6,-pt6-improvements-to-extreflection.html">ı</a> görmeliler.
<ol>
	<li>Namespaces</li>
	<li>Annountions</li>
	<li>Type Hint</li>
	<li>Reflection</li>
	<li>Delegate &amp; Event &amp; Lambda</li>
	<li>Function overloading</li>
	<li>Properties (Variable Get/Set)</li>
	<li>Extensions Methods &amp; Partial Class</li>
</ol>
<strong>1. Namespaces</strong>

Eğer bir framework yazıyorsanız birbirine benzeyen sınıf isimleri olması çok doğaldır. Bu durumlarda namespace'ler olması çok işe yarar. Neyse ki PHP 5.3'ten itibaren gelecek olan bir özellik. (Ref. <a href="http://marc.info/?l=php-internals&amp;m=118355320225178&amp;w=2">http://marc.info/?l=php-internals&amp;m=118355320225178&amp;w=2</a>)

<strong>2. Annountions</strong>

C#'ta buna Attribute denir. Amaç kod içine meta veriler sokmaktır. Ve bu verileri Reflection yöntemiyle dinamik olarak okuyarak işleme tabii tutmaktır.

Bir örnek ile açıklamak gerekirse, MVC yapısı kurduğumuzu düşünün. Her sınıfın bir sayfa her methodununda action/view işlemini yaptığını varsayalım. Action bazlı sayfa giriş yetkilendirmesine ihtiyacımız var. Bu sayfa eğer ödeme sayfası ise, sadece https olarak erişilmesi gerekiyor. Bunuda bir şekilde belirtmek gerekir. İşte bu gibi ihtiyaçları tanımlamak için annountions özelliğine ihtiyacımız var. Henüz resmi olarak desteklenmesede PHP genişletmeleriyle eklenebilir.
<pre class="prettyprint" style="padding-left: 30px;">@SimpleAnnotation
@SingleValuedAnnotation(true)
@SingleValuedAnnotation(-3.141592)
@SingleValuedAnnotation('Hello World!')
@SingleValuedAnnotationWithArray({1, 2, 3})
@MultiValuedAnnotation(key = 'value', anotherKey = false, andMore = 1234)</pre>
(Ref. <a href="http://code.google.com/p/addendum/">http://code.google.com/p/addendum/</a>)

<strong>3. Type Hint</strong>

Method parametreleri veya değişken tanımlarında, değişkenin tipini yazmak hem okunabilirliği arttırır. Hem de editörlerin kod tamamlama özelliğini daha sağlıklı yapılmasına imkan sağlar. Ayrıca hata yakalama işlemlerinde de büyük kolaylık sunar.

<strong>4. Reflection</strong>

Reflection dinamik olarak kod içerisinde gezinebilmeyi, kodu kısmen değiştirebilmeyi sağlar. Mesela; MVC'deki authentication işlemlerini sayfa sınıfının protected olan methodları için yap diyebiliriz.
<pre class="prettyprint" style="padding-left: 30px;">self::set_module_name($class_name);
self::set_action_name($method);

eval("\$class = new $class_name();");
$reflect = new ReflectionMethod($class_name, $method);
if ($reflect-&gt;isProtected()) {
$class-&gt;authentication();
}
call_user_method_array($method, $class, $method_arguments);</pre>
Ayrıca reflectionlar sayesinde <a href="http://en.wikipedia.org/wiki/Dependency_injection">Dependency Injection</a> diye adlandırılan mimariler yaratabiliriz. Dependency Injection, Bir kod parçasına dışarıdan müdahale etmek demektir. Örneğin bir scheduler uygulaması yazacaksınız. Bu schedulera "şu sınıfın şu methodunu" çalıştır demek için kullanabilirsiniz.

(Ref. <a href="http://tr2.php.net/reflection">http://tr2.php.net/reflection</a>)

<strong>5. Delegate &amp; Event &amp; Lambda</strong>

Delegate kavramı C# ile beraber hayatımıza girmiştir.  Aslında C programcılarının bildiği gibi delegate'ler, fonksiyon göstericileridir. C# gibi dillerde sınıflar arasında global kavramı olmadığı için bir sınıftan diğerine mesaj yaptırmak  gerekebiliyor bazı durumlarda. İtiraf etmem gerekir ki bu bizi event mimarilerine ve lambda operatörüne götürür.  Delegate kullanımı C'deki prototip tanımlanması gibidir.
<p style="padding-left: 30px;">public delegate function int myDelegate(int $x);</p>

Bu şu anlama gelir. Geri dönüş değeri int olan ve parametresi int olan fonksiyonu işaret et. Görüldüğü üzere bu tanım bize başka bir ihtiyaç daha doğurur. <strong>type hint</strong> ve <strong>method signs </strong>kavramları. Dinamik bir dilde bu kadar tip güvenli kod rahatsız etmiş olabilir. C# dilinde bunun çözümü lambda operatörüdür.

Lambda, kısaca değişken olarak tanımlanabilen process blockları demektir. İstenilen yerde yaratılır ve öldürülür.

<strong>6. Function overloading</strong>

Fonksiyon yazarken farklı parametrelerle aynı method adıyla yazabilme  durumudur function overloading.  Bilindiği üzere PHP dilinde parametre sınırı yok. İstenildiği kadar parametre girilebilir. Bu parametrelerin dinamikliği sayesinde, aynı method ismi ile farklı parametrelerde <strong>func_get_arg</strong> alınabilir. Fakat okunabilirliği zorlaştıracak bir kod bloğu oluşmasına sebep olur. Bunu desteklerken bu dinamik yapının kaldırılmasını elbette istemeyiz.

Method overloading yapabilmek için methodların imzasını tutmak gerekir. Bu imza parametrelerin tipleri ve geri donus deger tipleri ile birlikte oluşturulur.
<p style="padding-left: 30px;"><strong>int function fonk(int $b);
int function fonk(int $b, string $c);</strong>

Yukarıdaki örnek PHP'de syntax hatasına sebep olur.

<strong>7. Properties (Variable Get / Set)</strong>

Properties kavramı C# dilinde kullanılan Cross-Cutting yada Aspect oriented denilen bir teknolojidir. Amacı sınıf değişkenlerinin aldığı değerlerin arasına girmenin bir yolunu bulmaktır. Özellikle get ve set işlemlerinin arasına girmek türetilen sınıflarda overloading yöntemi ile farklı bir şekilde değer atanmasını veya değer kontrolunun yapılması burada sağlanabilir.<strong> </strong>
<p style="padding-left: 30px;"><strong>private</strong> $_item;
<strong>public property</strong> $Item
{
<strong>get</strong> { return $this-&gt;_item; }
<strong>set </strong>{ $this-&gt;_item = <strong>value</strong>; }
}

$this-&gt;Item = 4;

Yukarıdaki kod blogu gibi olmasada <a href="http://en.wikipedia.org/wiki/Aspect-oriented_programming">AOP</a> yontemiyle dolaylı olarak yapabilmek mümkün. Bunun için <a href="http://phpaspect.org">PHP Aspect</a>'ten faydalanılabilir. <cite><strong>
</strong></cite>

<strong>8. Extensions Methods &amp; Partial Classes
</strong>

Aslında bu iki özellik betik(script) olan bir dilde ne gerek var diye düşünebilirsiniz. Bu iki özellikte özellikle projelere dahil olan 3. parti yazılımların bakımını yaparken çok işimize yarar. Genellikle 3. parti yazılımları projenin içine dahil ederken ufak değişiklikler yapar ve projeyi bir bakıma çatallamış (fork) etmiş oluruz. Yeni versiyon geçişlerinde ise sıkıntı yaşarız. Bunu engellemek için başka bir yerde bu 3. parti yazılımların sınıflarını genişletebilsek (partial class) veya methodlarını aşırı yükleye bilsek (extensions methods) hayat daha güzel bir hale gelebilir. Peki bunu nasıl yaparız?

<strong>extend</strong> function <strong>string::</strong>is_null(<strong>string</strong> $value) { return ($value == null);  }

Yukarıdaki şekilde tanımlanabilir. string nesnesi için is_null adında bir method eklenmiş olur. Ve aşağıdaki şekilde çalıştırılabilir.

string $a = "merhaba";

if ($a::<strong>is_null</strong>()) { // biseyler yap }

Partial class yapısı ise, bir sınıfı içeriğini bir parçasını aynı isimde başka bir sınıfı tanımı yaratarak onun içine atamak demektir. Bakıldığında partial class ile extensions methods'ların bir farkı olmayabilir. C# kendi tasarımlarında partial classlar aynı assembly (paket) içerisinde olmasını ön koşul olarak koşar. Fakat bu durum extensions method mimarisinde zorunlu değildir.

Elbette bu iki özellik birleştirilerek daha iyi tasarlanabilir.

Benim PHP'nin yeni versiyonundan beklediklerim aklıma geldiği kadarıyla bu şekilde. Aslında bunların bir kısmı PHPv6 ya alındı. Bir kısmı ise bekliyor. Daha detaylı bilgiye, Derick Rethans'ın <a href="http://www.php.net/~derick/meeting-notes.html">toplantı notları</a>nda bulabilirsiniz. Bu konu ilginizi çektiyse, toplantı notlarının yapılacak listesine ve hangilerinin yapıldığına  <a href="http://wiki.pooteeweet.org/PhP60">buradan</a> erişebilirsiniz.

Benim aklıma gelenler şimdilik bunlar. Programlama dillerine ve Nesneye Yönelimli PHP'ye yönelik yazılarımı öğrendikçe burada paylaşmaya devam edeceğim...
