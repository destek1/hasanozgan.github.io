---
layout: post
title: Scala Geliştirme Ortamı ve Örnek Web Uygulaması
tags:
- Diğer
- eclipse
- eclipsify
- sbt
- scala
- scala ide
- scalate
- servlet
- ssp
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  _wp_old_slug: ''
---
Geçen yazımda Scala programlama diline kabaca <a href="/2011/02/scalaya-giris/">giriş yapmıştık</a>, bu yazımda ise bir web çatısı kullanımına geçmeden önce Scala geliştirme ortamını kurmaktan ve basit bir web uygulaması nasıl yazılır bundan söz etmek istiyorum.

Bu belgeleme ile aşağıdaki teknolojilerin içermektedir.
<ul>
	<li><a href="http://java.sun.com/javase/downloads/">Java Developer Toolkit</a></li>
	<li><a href="http://eclipse.org" target="_blank">Eclipse</a></li>
	<li><a href="http://www.scala-lang.org/downloads">Scala</a></li>
	<li><a href="http://scala-ide.org" target="_blank">Scala-IDE</a></li>
	<li><a href="http://code.google.com/p/simple-build-tool/" target="_blank">Simple Build Tool</a></li>
</ul>
<h3>Scala'nın Kurulumu</h3>
Scala, bilinen tüm popüler işletim sistemleriyle çalışmaktadır. Son sürümünü <a href="http://www.scala-lang.org/downloads">Scala'yı sitesinden</a> IzPack Installer versiyonunu indirerek kurabilirsiniz. Tabii bilgisayarınızda Java JDK'nın kurulu olması gerektiğini hatırlatayım.
<a href="files/2011/02/Screen-shot-2011-02-08-at-9.19.38-PM.png"><img class="aligncenter size-full wp-image-512" title="Scala Installer" src="/files//2011/02/Screen-shot-2011-02-08-at-9.19.38-PM.png" alt="" width="597" height="458" /></a>
<h3>Simple Build Tool (sbt) Kurulumu</h3>
SBT bilindiği üzere, proje yapılandırma aracıdır. Ivy ve Maven depolarından proje bağımlılıklarını hızlıca elde edebilirsiniz. Eklenti desteği ile <strong>embedded jetty</strong>, <strong>test işlemleri</strong> gibi çeşitli ihtiyaçlarınızı karşılayabilir sizde kendi eklentilerinizi yazabilirsiniz.
<h5>SBT'nin kurulumu;</h5>
Son kararlı sürüm olan 0.7.4'ü <a href="http://code.google.com/p/simple-build-tool/downloads/detail?name=sbt-launch-0.7.4.jar">buradan</a> ya da <a href="http://code.google.com/p/simple-build-tool/downloads/list">projenin sitesinden</a> en güncel sürümünü indirebilirsiniz.
<h5>Neden SBT?</h5>
SBT tamamiyle Scala diliyle yazılmıştır. Ve bağımlılık yönetiminde Maven ve Ivy'i depoları kullanır. Isterseniz manuel olarak yeni bir depo ekleyebilir yada cikartabilirsiniz. SBT'nin gelişmiş bir console arayüzü vardır. SBT komutları iki çeşittir. Bir doğal komutları, ikincisi ise pluginlerle gelen komutlar ve ikinci olarakta <strong>action</strong> diye adlandırılan plugin komutlarıdır. Bu komutların çağrısı yapılırken özel anlamlara gelen ön ekler alabilirler. Bu sayede komutlar daha güçlendirilebilir.
{% highlight sh %}
$ sbt help
[info] Building project HelloWeb 1.0 against Scala 2.8.1
[info]    using HelloProject with sbt 0.7.4 and Scala 2.7.7
You may execute any project action or method or one of the commands described below.
Available Commands:
   <action name> : Executes the project specified action.
   <method name> <parameter>* : Executes the project specified method.
   <processor label> <arguments> : Runs the specified processor.
   ~ <command> : Executes the project specified action or method whenever...
   < file : Executes the commands in the given file.  Each command should...
   + <command> : Executes the project specified action or method for all...
   ++<version> <command> : Changes the version of Scala building the project...
   * : Prefix for commands for managing processors.  Run '*help' for details.
   ! : Prefix for history commands.  Run '!' for history command help.
...
{% endhighlight %}

Sbt'nin konfigürasyon dosyası yine Scala kodları yani <strong>Trait</strong> türünde sınıflardan türetilerek yapılır. Türediği Trait sınıfına ve yüklendiği eklentilere göre projenin türü ve kullanılacak actionlar belli olur.

Yukarıda adından söz ettiğimiz bu konular makalenin sonunda yaratacağımız örnek proje ile daha iyi anlayacaksınız.
<h5>Unix ve MacOs Sistemleri için <em>sbt.sh</em> dosyası</h5>
{% highlight sh %}
java -Xmx512M -Xss2M -XX:+CMSClassUnloadingEnabled -jar `dirname $0`/sbt-launcher.jar "$@"
{% endhighlight %}
<h5>Windows Sistemleri için <em>sbt.bat</em> dosyası</h5>
{% highlight sh %}
set SCRIPT_DIR=%~dp0
java -XX:+CMSClassUnloadingEnabled -XX:MaxPermSize=256m -Xmx512M -Xss2M -jar "%SCRIPT_DIR%\sbt-launcher.jar" %*
{% endhighlight %}
<h3>Scala-IDE Kurulumu</h3>
Scala IDE projesi Eclipse platformu üzerinde geliştirilene daha çok yeni olan bir projedir. Eksikleri olsada, Eclipse sayesinde bu açıklar zamanla toparlanacaktır. Scala IDE'yi kurmak için bilgisayarınızda Eclipse'in kurulu olduğunu varsayıyorum.
<center><iframe title="YouTube video player" width="640" height="390" src="http://www.youtube.com/embed/PtkNg4mK4NY" frameborder="0" allowfullscreen></iframe></center>
Eclipse, Scala-IDE eklentisinin kurulumu için aşağıdaki video işinize yarayacaktır. Kendini eclipse sürümünüze uygun eklentinin adresine ise <a href="http://download.scala-ide.org/">buradan</a> erişebilirsiniz.
<h3>Scala İle Basit Bir Web Uygulaması Yaratmak</h3>
<h5>Proje Oluşturma</h5>
Örnek uygulama adımlarını Linux ve MacOS sistemlerinde çalışacak biçimde anlatacağım. <strong>HelloWeb</strong> isimli dizini oluşturduktan sonra dizinin içine giriyor ve <strong>sbt</strong> komutunu çalıştırıyoruz. Proje dizini ve dosyasını bulamazsa, yeni proje yaratmak isteyip istemediğimizi soruyor. Yeni proje yaratma adımları için aşağıdaki şekilde tamamladıktan sonra sbt konsolundan <strong>exit</strong> komutuyla çıkıyoruz.

{% highlight sh %}
$ mkdir HelloWeb &amp;&amp; cd HelloWeb
$ sbt
Project does not exist, create new project? (y/N/s) y
Name: Hello Web
Organization: Hasan Ozgan
Version [1.0]:
Scala version [2.7.7]: 2.8.1
sbt version [0.7.4]:
Getting Scala 2.7.7 ...
:: retrieving :: org.scala-tools.sbt#boot-scala
confs: [default]
2 artifacts copied, 0 already retrieved (9911kB/35ms)
Getting org.scala-tools.sbt sbt_2.7.7 0.7.4 ...
:: retrieving :: org.scala-tools.sbt#boot-app
confs: [default]
15 artifacts copied, 0 already retrieved (4096kB/71ms)
[success] Successfully initialized directory structure.
Getting Scala 2.8.1 ...
:: retrieving :: org.scala-tools.sbt#boot-scala
confs: [default]
2 artifacts copied, 0 already retrieved (15118kB/72ms)
[info] Building project Hello Web 1.0 against Scala 2.8.1
[info]    using sbt.DefaultProject with sbt 0.7.4 and Scala 2.7.7
> exit
{% endhighlight %}

Projeyi yarattığımızda aşağıdaki gibi bir dizin ağacı göreceksiniz. Bu dizin ağacında <strong>project</strong> isimli dizinde proje yapılandırma işlemlerimizi yapıyoruz. Projemizin kaynak kodları ise <strong>src/main/scala</strong> dizinin altında yazıyoruz. Henüz uygulamamız web uygulaması olarak yapılandırılmadığı için <strong>src/main/webapp</strong> dizini mevcut değil. Yazının ilerleyen bölümlerinde bu dizini ve konfigürasyonları elle yapılandıracağız. :)

{% highlight sh %}
HelloWeb$ tree
   .
   ├── lib
   ├── project
   │   ├── boot
   │   └── build.properties
   ├── src
   │   ├── main
   │   │   ├── resources
   │   │   └── scala
   │   └── test
   │       ├── resources
   │       └── scala
   └── target
{% endhighlight %}

<h5>Projenin Yapılandırılması</h5>
Şimdi örnek web uygulamamız için projemizi yapılandırmaya başlayalım. Sbt kendini çalıştırdığında <strong>project/build/*.scala</strong> dizini altında <strong>BasicScalaProject</strong> abstract sınıfından türemiş bir sınıf arar. Yapılandırma işlemleri bu sınıfın içinde olur.

Şimdi gelin bizde böyle bir sınıf tanımı yapalım.

{% highlight sh %}
HelloWeb$ mkdir build
HelloWeb/build$ vim HelloProject.scala
{% endhighlight %}

{% highlight scala %}
import sbt._

class HelloProject(info: ProjectInfo) extends DefaultWebProject(info)
{
    override def libraryDependencies = Set(
        "javax.servlet" % "servlet-api" % "2.5" % "provided"
        "org.mortbay.jetty" % "jetty" % "6.1.22" % "test-&gt;default"
    ) ++ super.libraryDependencies
}
{% endhighlight %}
<strong>project/build/HelloProject.scala</strong>

Şimdi uygulamamızı yazmaya geçmeden önce projemizi eclipse taşıyalım. Bunun için, <strong>Eclipsify</strong> isimli sbt eklentisini kurmamız gerekiyor. SBT projesine eklentileri tanımlamakta çok kolay.
Öncelikle dizinini eklememiz gerekiyor.

{% highlight sh %}
HelloWeb$ mkdir -p project/plugins
HelloWeb/project/plugins$ vim HelloPlugins.scala
{% endhighlight %}

{% highlight scala %}
import sbt._

class HelloPlugins(info: ProjectInfo) extends PluginDefinition(info) {
    lazy val eclipse = "de.element34" % "sbt-eclipsify" % "0.7.0"
}
{% endhighlight %}
<strong>project/plugins/HelloPlugins.scala</strong>

Son olarakta HelloProject.scala sınıfımıza eklentiyi tanımlamamız gerekiyor. Sınıfımız aşağıdakine benzemeli.

{% highlight scala %}
import sbt._
import de.element34.sbteclipsify._

class HelloProject(info: ProjectInfo) extends DefaultWebProject(info) with Eclipsify
{
    override def libraryDependencies = Set(
        "javax.servlet" % "servlet-api" % "2.5" % "provided"
        "org.mortbay.jetty" % "jetty" % "6.1.22" % "test-&gt;default"
    ) ++ super.libraryDependencies
}
{% endhighlight %}

Artık uygulamamızı yazmaya hazırız. Yapmamız gereken son bir işlem var. SBT projemizi Eclipse'in anlayacağı hale sokmak. Bunun için önce javax.servlet ve jetty bağımlılıklarımızı güncellememiz gerekiyor. Bunu yapmamızı sağlayan komut ise <strong>update</strong>. Bu işlemi yaptıksan sonra <strong>eclipse</strong> isimli yeni <em>action</em> görmeniz gerekiyor.

{% highlight sh %}
sbt update
[info] Recompiling plugin definition...
[info] 	  Source analysis: 1 new/modified, 0 indirectly invalidated, 0 removed.
[info]
[info] Updating plugins...
[info] downloading http://scala-tools.org/repo-releases/de/element34/sbt-eclipsify/0.7.0/sbt-eclipsify-0.7.0.jar ...
{% endhighlight %}

sbt actions komutunda listenen action listesinin içinde eclipse'ei görmeniz gerekiyor. Eğer görüyorsanız eclipse proje dosyasını oluşturmak için;

{% highlight sh %}
HelloWeb$ sbt eclipse
[info] Building project HelloWorld 1.0 against Scala 2.8.1
[info]    using Project with sbt 0.7.4 and Scala 2.7.7
[info]
[info] == eclipse ==
[info] Creating eclipse project...
[info] == eclipse ==
[success] Successful.
[info]
[info] Total time: 0 s, completed Feb 9, 2011 5:59:41 PM
[info]
[info] Total session time: 1 s, completed Feb 9, 2011 5:59:41 PM
[success] Build completed successfully.
{% endhighlight %}

Artık işlemi tamamladık. Şimdi Eclipse açarak, projeyi import edebilirsiniz. 
<center>
<table>
<tbody>
<tr>
<td><a href="/files//2011/02/HelloWeb-Import.png"><img class="aligncenter size-medium wp-image-589" title="HelloWeb Project Import" src="/files//2011/02/HelloWeb-Import-264x300.png" alt="HelloWeb Project Import" height="300" /></a></td>
<td>&nbsp;</td>
<td><a href="/files//2011/02/HelloWeb-Tree.png"><img src="/files//2011/02/HelloWeb-Tree-264x300.png" alt="" title="HelloWeb Tree" width="264" height="300" class="alignleft size-medium wp-image-590" /></a></td>
</tr>
</tbody>
</table>
</center>

Son olarak Eclipse'ten SBT'yi çalıştırmak için External Tool Configuration seçeneğinden tanımlamamız gerekiyor. Aşağıda örnek ayarlara ait ekran görüntüsünü bulabilirsiniz.
<center>
<a href="/files//2011/02/HelloWeb-Extarnal.png"><img src="/files//2011/02/HelloWeb-Extarnal-300x205.png" alt="" title="HelloWeb Extarnal" width="300" height="205" class="aligncenter size-medium wp-image-593" /></a>
</center>
Artık web uygulamamızı yazmaya başlayabiliriz.
<h5>Scala Servlet</h5>
Scala'nın java mimarileriyle çalışabildiğinden daha önce söz etmiştim. Bu nedenle bir scala web uygulaması yazmak, bir java web uygulaması yazmaktan pek farklı değildir. Scala'da servlet sınıfları kullanılarak yazılabilir. Aşağıda basit bir servlet sınıfı bulunmaktadır. Scala dilinde XML aynı bir String gibi bir tiptir. Örnek scala kodumuzun java'dan tek farkı HTML tipinin parametre olarak verilebilmesidir.

{% highlight scala %}
package com.hasanozgan.web

import java.io._
import javax.servlet.http.{HttpServlet, HttpServletRequest, HttpServletResponse}

class HelloServlet extends HttpServlet
{
    override def doGet(req: HttpServletRequest, res: HttpServletResponse)
    {    
        doRequest(req, res) 
    }    

    override def doPost(req: HttpServletRequest, res: HttpServletResponse)
    {    
        doRequest(req, res) 
    }    

    private def doRequest(req: HttpServletRequest, res: HttpServletResponse)
    {    
        res.getWriter().print(<html>
              <head>
                <title>Hello World</title>
              </head>
              <body>
                <h1>Hello from Scala!</h1>
              </body>
            </html>)
    }    
}
{% endhighlight %}
<strong>src/main/scala/com/hasanozgan/web/HelloServlet.scala</strong>

Şimdi wepapp ve WEB-INF dizinlerini yarartmaya ve webapp/WEB-INF/web.xml dosyasını oluşturmamız gerekiyor. Aşağıdaki örnek bir web.xml dosyası mevcut.

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="http://java.sun.com/xml/ns/javaee" 
    xmlns:web="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" 
xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
   version="2.5">

  <servlet>
    <servlet-name>HelloServlet</servlet-name>
    <servlet-class>com.hasanozgan.web.HelloServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
  </servlet>

  <servlet-mapping>
    <servlet-name>HelloServlet</servlet-name>
    <url-pattern>/index</url-pattern>
  </servlet-mapping>

  <welcome-file-list>
    <welcome-file>index</welcome-file>
  </welcome-file-list>

</web-app>
{% endhighlight %}
<strong>src/main/webapp/WEB-INF/web.xml</strong>

Uygulamayı çalıştırmak için ise <strong>sbt ~jetty-run</strong> komutunu çalıştırmamız yeterlidir.

{% highlight sh %}
HelloWeb$ sbt ~jetty-run
{% endhighlight %}

Not: <b>sbt <font color="red">~</font>jetty-run</b> komutu ile <b>sbt jetty-run</b> komutu arasında şöyle bir fark bulunur. Eğer bir komut "<strong>~</strong>" işareti ile başlarsa projenin dosyalarında bir değişiklik olursa proje tekrar derlenir.

<h5>Scala Server Pages (Scalate)</h5>
Scala dünyasında Quick & Dirty birşeyler yapmak isteyenler için JSP'ye benzer bir template engine kütüphanesi mevcut. <a href="http://scalate.fusesource.org/">Scalate (Scala Template)</a> isimli bu proje gerçktende çok başarılı template modelleri ile geliyor. Bu modellerden benim tercihim SSP yani Scala Server Pages modeli. Zevkinize göre diğer modellere de göz atabilirsiniz. 
<ol>
	<li>
Önce sbt proje sınıfımıza(HelloProject.scala) scalate için gerekli olan tanımları(<em>"org.fusesource.scalate" % "scalate-core" % "1.2"</em>) yapmamız gerekiyor. Ayrıca, jetty'nin portunu nasıl değiştirebileceğimizide görelim.

{% highlight scala %}
import sbt._

class HelloProject(info: ProjectInfo) extends DefaultWebProject(info)
{
     val jettyPort = 8090

    override def libraryDependencies = Set(
        "org.fusesource.scalate" % "scalate-core" % "1.2",
        "javax.servlet" % "servlet-api" % "2.5" % "provided"
        "org.mortbay.jetty" % "jetty" % "6.1.22" % "test-&gt;default"
    ) ++ super.libraryDependencies
}
{% endhighlight %}

Proje ile değişiklikler yaptıktan sonra <strong>sbt update</strong> komutunu çalıştırmayı unutmayın.
       </li>
	<li>
Şimdi <strong>web.xml</strong> dosyamızda Servlet Filter'ı tanımlamamız gerekiyor.
{% highlight xml %}

  <!-- START: Scalate config -->
  <servlet>
    <servlet-name>TemplateEngineFilter</servlet-name>
    <servlet-class>org.fusesource.scalate.servlet.TemplateEngineServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>TemplateEngineFilter</servlet-name>
    <url-pattern>*.ssp</url-pattern>
  </servlet-mapping>
  <!-- END: Scalate config -->
{% endhighlight %}
       </li>
	<li>
Şimdi son olarak <strong>index.ssp</strong> dosyamızı yazalım. SSP ile ilgili daha detaylı örnek arayanlar <a href="https://github.com/scalate">scalate'in github hesabından</a> <a href="https://github.com/scalate/scalate/tree/master/samples/scalate-sample">örnek kodları</a> inceleyebilir.
{% highlight scala %}
<html>
    <head>
    <title>Scala Server Pages</title>
    </head>
    <body>
<%
    var username: String = "";
    if (request.getMethod().equals("POST")) {
        username = request.getParameter("username")
        out.println("Hello, "+username);
    }    
%>
        <form method="post">
            <input type="text" name="username" value="${username}"/>
            <input type="submit" value="Ok" />
        </form>
    </body>
</html>
{% endhighlight %}
       </li>
</ol>

Böylece bir Scala Server Page koduda yazmış olduk.

<h5>Kaynak Kod</h5>
Örnek uygulamanın kaynak kodlarına aşağıdaki linkten erişebilirsiniz.
<a href="/files/2011/02/HelloWeb.tgz">Scala Web Uygulaması Kaynak Kodları</a>

Özetleyecek olursak, Sbt ile Scala projesi yaratma ve basit web uygulamarı yazmayı adımlarını görmüş olduk. Benim için bu yazı gerçekten yorucu ve uzun oldu, umarım işinize yaramıştır. Bir sonraki yazımızda ise veritabanı işlemlerinden söz etmeyi planlıyorum. RDBMS (mySQL) ve NOSQL (mongoDB) örnekleri içeren bir yazı olacak. Bu hafta veritabanı işlemlerine de bir giriş yaptıktan sonra, Lift Web Framework ile adım adım örnek bir web uygulaması geliştireceğiz.. (Benim aklımdan Grupon yada Hacker News klonu yapmak geçiyor. Eğer başka bir öneriniz varsa lütfen benimle paylaşın)
