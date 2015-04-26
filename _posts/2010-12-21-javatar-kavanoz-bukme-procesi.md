---
layout: post
title: jAvatar - Kavanoz Bükme Procesi
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _wp_old_slug: ''
  _edit_last: '2'
---
Linux terminalde çalışırken, aradığınız bir sınıfın $CLASSPATH'teki hangi jar dosyasında olduğunu bulmanızı sağlar.

Bash programlama hakkında çok fazla bilgiye sahip değilim. Konunun uzmanlarından güzel fikirler ve düzeltmeler bekliyorum. (-: Kısacası geliştirmeye açıktır. İstediğiniz gibi kodu evirip çevirip bu oyuncakla oynayabilir, yeni kavanoz bükme tekniklerini paylaşabilirsiniz. 

<strong>Kullanım şekli;</strong>

<em>$ javatar &lt;className&gt;</em>

{% highlight bash %}
#!/bin/bash
echo -ne "\033[1mjAvatar ver. 1.0.3 (by meddah)\n\033[0m";
echo -ne "May the 'Jar Bender' force be with you!\n";

export source=$1
files=();
classes=();

#resolver
for file in `echo $CLASSPATH|tr ":" "\n"|grep -i jar`;
do
    for class in `jar -tvf $file|awk '{print $8}'|grep -e $source`;
    do
        if [[ $files != *$file* ]]; then
            files+="$file ";
        fi

        classes+="$file:$class ";
    done
done

#dispatcher
for file in $files; do
    echo -e "\033[1m$file\033[0m";

    for class in $classes; do
        if [[ $class == *$file* ]]
        then
            echo -n "    ";
            echo $class|tr ":" " "|awk '{print $2}';
        fi
    done
done

echo -ne "\n";

{% endhighlight %}
