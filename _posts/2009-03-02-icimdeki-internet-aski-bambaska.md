---
layout: post
title: İçimdeki İnternet Aşkı Bambaşka!..
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Hava bahardan kalma ve güneş dünyaya gülümsüyordu. Günlerden pazar günüydü. Dışarı çıkma planları yapmış, bloguma yeni bir yazı girişi yapıyordum ki, veritabanı çok fazla bağlantı hatası vermeye başlayınca "Ne oluyor laan!" cümlesi ağzımdan çıkı verdi. Sunucunu loglarına bakınca saniyede 50-100 arası istek olduğunu görünce saldırı olduğunu düşündüm. (Normalde sunucuma bu kadar istek gelmez!) Sonra incelediğimde sorunun sebebinin kissa.be servisi olduğunu gördüm. Kissa.be yurtdışında az-buçuk tanınan bir servis olduğu için neden bu kadar istek geldiğine baktım. Halen saldırı olduğunu düşünüyordum fakat inceleyince gördümki, kissa.be'yi kullanan kişi Çin'deki bir Porno Forumuna kissa.be linki vermiş. Ve bu yazıyı yazarken Uniq istek 150.000 civarındaydı. Sunucum ve benim için çok fazla olan bu isteği kara listeye almak istemiyordum. Sonuçta kissa.be bir servisti herşeye garanti veriyordu.

Peki bu sorunu nasıl çözdüm? Sihirli sözcükleri söylediğinizi duyar gibiyim. Evet Memcached! Hayat kurtaran asrın buluşu icat. Hemen memcache sisteme aktif ettim. İnsert işlemlerinide bir  havuza soktum. SQL sorguları bir havuzda toplu olarak güncelleniyor. Sorun çözüldü böylece, kissa.be servisi icin yapmayi bile dusunmedigim stress testi boylece gerceklesti.

Evet güzel pazar günüm bu işle uğraşarak gitti. :) Peki pişman mıyım? Hayır! Kızgın mıyım? Evet Kendime kızgınım!. Kodları bu hafta daha ciddi bir şekilde yeniden düzenleyeceğim. Her geçen gün biraz daha şekillenen Joy Framework mimarisine taşımaya karar verdim. İnterneti ve yüzbinlerce (pornocu) insanın farkında olmadan benim sitemi kullanmaları çok eğlenceliydi. Apache log'u her an aktığını ne zamandır görmüyordum. :)

Evet sıradaki sınavlar için  hazırım :)
