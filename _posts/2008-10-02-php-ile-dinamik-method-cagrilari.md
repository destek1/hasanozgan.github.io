---
layout: post
title: PHP ile Dinamik Method Çağrıları
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Dinamik method çağrısı, parametrelerinin uzunluğunu bilmediğiniz bir methoda çağrı yapmak için kullanılır. Hangi durumlarda buna ihtiyacımız olur derseniz; MVC'ler buna iyi bir örnektir. Yazımın ikinci bölümünde söz edeceğim dinamik obje yaratma durumlarındada çok işe yararlar. Peki az laf çok örnek yaparak konuyu özetleyeyim.

Diyelim ki;

http://example.com/<span style="color: #993300;"><strong>blog</strong></span>/<span style="color: #808000;"><strong>categories</strong></span>/<strong><span style="color: #3366ff;">200810</span></strong>/<span style="color: #000080;"><strong>general</strong></span>

yukarıdaki gibi bir çağrıyı doğru şekilde yönlendirmemiz gerekiyor. İşte böyle bir durumda dinamik method çağrısı çok işe yarar.

class <span style="color: #993300;"><strong>blog </strong></span>extends <strong>controller</strong>

{

function <span style="color: #808000;"><strong>categories</strong></span>(<span style="color: #3366ff;"><strong>$date</strong></span>, <span style="color: #000080;"><strong>$cat_name</strong></span>)

{....}

}

Peki bunu nasıl yapıyoruz?
<ul>
	<li>call_user_func</li>
	<li>call_user_func_array</li>
	<li>call_user_method</li>
	<li>call_user_method_array</li>
</ul>
Yukarıdaki 4 fonksiyon adı (anahtar kelime) yeterlidir sanırım. Peki yukarıdaki örneğimizde bu çağrı nasıl yapılıyor ona bakalım.

URL parse edildikten sonra;<span style="color: #000080;"><strong> </strong><strong></strong></span>

<strong>call_user_method_array</strong>(<span style="color: #808000;"><strong>$method</strong><strong></strong></span>, <span style="color: #993300;"><strong>$class</strong></span>, <span style="color: #3366ff;"><strong>$<span style="color: #000080;">args</span></strong></span><span style="color: #000080;"><strong></strong></span>);

method çağrısı ile gerçekleştirebilirsiniz.

call_user_xxx methodlarını <strong>__construct</strong> methodu için kullanamazsınız. Yani olurda benim gibi dinamik olarak obje yaratmak isterseniz bu methodlar işe yaramaz. İşte bu durumlarda işinize yarıyacak bir method örneği vereceğim.

$db-&gt;comment = <strong>using</strong>("dal.comment", $db);

Biraz methodun ne yaptığını açıklamam gerekir sanırım. Biliyorsunuz PHP 5.3 ile beraber namespace kavramı hayatımıza girdi. Kendi geliştirmekte olduğum framework'te <strong>import</strong> işlemleri için çok basit bir şekilde çalışan bir namespace sistemi oluşturdum. using ile ise; aynı isime ait iki sınıf, kazaren çakışması durumunu engellemek için yazmıştım. İlk parametre sınıfın paket bilgisi ikincisinde ise, <strong>__construct </strong>methodunun aldığı parametreler söz konusu. İşte bu işi <strong>call_user_XXX</strong> kullanmadan yapmanın yolu;

<pre>
    function using($class)
    {
        require_once(_get_class_path($class));
        $class_name = _find_class_name($class);

        $args_count = func_num_args();

        $args = "";
        for ($i = 1; $i < $args_count; $i++)
        {
            eval("\$arg_{$i} = func_get_arg($i);");
            $args .= "\$arg_{$i},";
        }
        $args = rtrim($args, ",");

        eval("\$obj = new $class_name($args);");
        return $obj;
    }

</pre>
