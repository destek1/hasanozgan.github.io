---
layout: post
title: Adım Adım Ruby - 2 -
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Eğer kendi kendinize birşey öğreniyorsanız ve birşeyler öğrenirken sıkılıyorsanız bunun sebebi kesinlikle bilinmeyenin göz korkutmasıdır. Yani kitaplar şimdi bunu yapıyoruz şunu kullanacağız. Bir sürü bilinmeyen bir sürü soru işareti ve sonunda oluşan kocaman bir korku ortaya çıkar. Eğer sabır da göstermezsek sonunda pes edip öğrenilen şeyden vazgeçeriz. Bu sebeple yeni birşey öğrenirken geneline bir bakış atmak. Ne neymiş, neden kullanılırmış anlamak isterim. İşte bu sebeple bu yazıda ruby'i ruby yapan şeylerden ve genel özelliklerinden söz edeceğim. Bunların hızlıca üzerinden geçeceğim ama verdiğim bilgiler referans niteliğinde olacak. İleride bu konuda örnekler verdiğimde kodu anlamanıza büyük kolaylık sağlayacak.

<strong>Ruby'i Seçmeniz İçin Birkaç Neden?</strong>
<ul style="list-style: disc; margin-left: 18px;">
	<li>Ruby tamamen nesne yönelimli bir programlama dilidir.</li>
	<li>Operatörleri yeniden yazmanıza izin verir.</li>
	<li>Bir sınıfın kaynağına dokunmadan bir metodu yeniden yazmanıza izin verir.</li>
	<li>İşinizi kolaylaştıracak birçok operatöre sahiptir.</li>
	<li>Eğer C biliyorsanız yeni kütüphaneler yazarak dili genişletebilirsiniz.</li>
	<li>Blok mimarisi sayesinde bir metoda bir kod işlemi aktarabilir ve birçok şeyi tek satırda yapabilirsiniz.</li>
	<li>Betik dilidir. Yapılan değişiklikleri anında siteye yansıtır. Java gibi jar dosyaları ile boğuşmazsınız.</li>
	<li>String ve RegEx sınıfları sayesinde hızlı hareket etmenizi sağlar. Programcının menfaatine iş yapar ve çevir bir dildir.</li>
	<li>Platform bağımsızdır. Birçok platformda yazılan kodunuz çalışır.</li>
	<li>Dinamik değişken tanımlama.</li>
	<li>Birçok dilden miraslar aldığı için yazılımcının alışkanlıklarına göre kod yazım esnekliği.</li>
	<li>Yorumlanan bir dildir.</li>
</ul>
<strong>Genel Yazım Kuralları</strong>
<ul style="list-style: disc; margin-left: 18px;">
	<li>Yorum Satırları
# karakteri, bulunduğu satırı, satır sonuna(EOL) kadar yorum satırına dönüştürür.
Yorumlayıcı bu satırı görmezden gelir.
'=begin' ve '=end' arasında kalan satırları yorumlayıcı görmezden gelir.</li>
	<li>Deyim Sonlandırma
Deyim sonlandırma işlemi ya satır sonu ya da eğer aynı satırda birkaç deyim kullanılacaksa (;) (noktalı virgül) işaretidir.</li>
	<li>Sınıf ve Modül tanımları büyük harfle başlamalıdır. (Ör: REXML::Element)</li>
	<li>Değişken tanımları küçük harfle olmalıdır. Değişkenler ilk tanımlamada değer almalıdır. Tek başına yazılamaz. (Ör: foo = 2)</li>
	<li>Method tanımları küçük harfle başlar. (Ör: Math:cos(x))</li>
	<li>Sabitlerin tamamı büyük harf olmalıdır. (Ör:Math:PI)</li>
</ul>
<strong>Reserve Kelimeler</strong>
<pre>alias   and     BEGIN   begin   break   case    class   def     defined
do      else    elsif   END     end     ensure  false   for     if
fin      module  next    nil     not     or      redo    rescue  retry
return  self    super   then    true    undef   unless  until   when
while   yield</pre>
<strong>Veri Tipleri</strong>
Sayı(numbers),
String,
Aralık(ranges),
RegEx, Sembol(symbol),
Diziler(arrays),
Sözlükler(hashes)
Prosedur (proc)

<strong>Sayılar</strong>
Bignum (1234567890)
Fixnum (1234)
Float (1234.56)
Hex (0xFFFF)
Binary (0b0101010)
Octal (0377)
?a       ASCII karakterinin sayısal degeri
?\C-a    Control-a karakterinin sayısal degeri
?\M-a    Meta-a karakterinin sayısal degeri
?\M-\C-a Meta-Control-a karakterinin sayısal degeri

<strong>String</strong>
%() ile baslayan karakterleri asagidakiler string karakteridir.  %[], %!!, %@@, vb.

'araya deger girilemez'
"#{degisken}, ve backslash karakter alir\n"
%q(araya deger girilmez)
%Q(araya deger ve backslash karakteri alir)

%(araya deger ve backslash karakteri alir)

`echo komut satırı ara deger ve backslash karakterleri alir.` =&gt; `ls` denemek ister misiniz?
%x(echo komut satırı ara deger ve backslash karakterleri alir.)

Backslash
\t (tab),
\n (newline),
\r (carriage return),
\f (form feed),
\b (backspace),
\a (bell),
\e (escape),
\s (whitespace),
\nnn (octal),
\xnn (hexadecimal),
\cx (control x),
\C-x (control x),
\M-x (meta x),
\M-\C-x (meta control x)

<strong>Semboller</strong>

Sozluk(hash) ifadelerinde kullanmak icin idealdir. C'de enum'a benzer fakat deger almazlar.(Bazi ozel sembol tanımlama tipleri alır) Asagida orneklerle açıklamaya çalıştım.

:sembol                         =&gt; :sembol
:'#{"ara"} deger almaz'  =&gt; :"#{"ara"} deger almaz"
:"#{"ara"} deger"     =&gt; :"ara deger"
%s(#{"ara"} deger almaz) =&gt; :"#{"ara"} deger almaz"

<strong>Aralıklar</strong>
1..10 =&gt; 1'den 10'a kadar (10 dahil)
1...10 =&gt; 1'den 10'a kadar (10 haric)
'a'..'z'
'a'...'z'
(1..10)  === 5   =&gt; dogru
(1..10)  === 10  =&gt; dogru
(1...10) === 10  =&gt; yanlis
(1..10)  === 15  =&gt; yanlis

<strong>Diziler</strong>
[1, 2, 3]
%w(foo bar baz)
%W(foo bar baz #{var})

Dizilerde index degerleri negatif deger alabilir. Bu dizinin orjinini sondan baslatir.

<strong>Sözlükler (Hashes)</strong>

{'bir'=&gt;1, 'iki'=&gt;2, 'uc'=&gt;3}
{ expr =&gt; expr...}

<strong>Değişkenler ve Sabitler</strong>

4 tip değişken etki alanı vardır. Değişkenin isminin başına gelen özel işaretlerle ve etki alanına göre yorumlayıcı tarafından anlaşılır.

1) Global değişkenler
Tanım: $global_variable = 0
Uygulama boyunca yaşarlar. Özellikle ön tanımlı global değişkenler ile kullanılır.
Hepsi ($) işareti ile başlar.

2) Sınıf Değişkenleri
Tanım: @@class_variable = 0
Sınıf her yeni yaratılan örnekte bu değişkenin değeri yeni nesneye aktarılır. Singleton kalıbında kullanılabilir. Bir örnekle açıklayalım;
<blockquote>
<pre><code class="ruby">class Boom

  @@class_counter = 0
  def initialize
    @instance_counter = 0
  end

  def explode
    @@class_counter += 1
    @instance_counter += 1
    puts "@@class_counter =&gt; #{@@class_counter}"
    puts "@instance_counter =&gt; #{@instance_counter}"
  end
end

d1 = Boom.new
d1.explode()
d1.explode()

d2 = Boom.new
d2.explode()
</code></pre>
</blockquote>
3) Örnekleme(instance) Değişkenleri

4) Yerel Değişkenler
