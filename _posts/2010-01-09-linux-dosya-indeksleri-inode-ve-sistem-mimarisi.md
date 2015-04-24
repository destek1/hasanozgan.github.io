---
layout: post
title: Linux Dosya Indeksleri (inode) ve Sistem Mimarisi
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  _wp_old_slug: ''
---
<style>
	.info {
		border: none;
		margin: 3px;
		text-align: left;
		width: 500px;
	}
</style>

<p>Birkaç gündür <a href="http://kissa.be">kissa.be</a> servisinin bulunduğu sunucu, diskte yer yok hatası nedeniyle düzgün bir şekilde hizmet veremiyordu. Durumu farkeder farketmez, diskteki yerimi kontrol ettiğimde gördüm ki; diskin %80'lik bir bölümü halen boş. Sorunun sunucu hizmeti aldığım firmayla görüşünce, anlaşıldı ki, diske format atarken varsayılan değerlerini aynen kabul ettiğim dosya indekslerimin (inode size) tükendiği için bu hatayı aldığım anlaşıldı.</p>

<p>Diskte mevcut inode sayısını görmek için;</p>

<blockquote>
	<table class="info">
		<tr>
			<td colspan="5"><p>root@localhost:~#<strong> df -ih</strong></p></td>
		</tr>
		<tr>
			<th>Filesystem</th>
			<th>Inodes</th>
			<th>IUsed</th>
			<th>IFree</th>
			<th>IUse%</th>
			<th>Mounted on</th>		
		</tr>
		<tr>
			<td>/dev/sda</td>
			<td>680K</td>
			<td>21K</td>
			<td>660K</td>
			<td>3%</td>		
			<td>/</td>		
		</tr>	
		<tr>
			<td>/dev/sdc</td>
			<td>1.3M</td>
			<td>25K</td>
			<td>1.2M</td>
			<td>2%</td>		
			<td>/files	</td>		
		</tr>
	</table>
</blockquote>

<p>Diskteki mevcut boş alanı görmek için ise;</p>

<blockquote>

	<table class="info">
		<tr>
			<td colspan="5"><p>root@localhost:~#<strong> df -h</strong></p></td>
		</tr>
		<tr>
			<th>Filesystem</th>
			<th>Size</th>
			<th>Used</th>
			<th>Avail</th>
			<th>Use%</th>
			<th>Mounted on</th>		
		</tr>
		<tr>
			<td>/dev/sda</td>
			<td>11G</td>
			<td>741M</td>
			<td>9.5G</td>
			<td>8%</td>
			<td>/</td>		
		</tr>	
		<tr>
			<td>/dev/sdc</td>
			<td>4.8G</td>
			<td>960M</td>
			<td>3.6G</td>
			<td>21%</td>
			<td>/files</td>		
		</tr>
	</table>
</blockquote>

<p><a href="http://kissa.be">Kissa.be</a> resim ve metin gibi dosyaları saklamanıza yarayan bir servis olduğu için çok küçük oranlarda çok fazla dosya bulundurabiliyor bünyesinde. Bu da dosya indeks limitimin hızlı bir şekilde tükenmesine neden olmuştu. </p>

<p><a href="http://kissa.be">Kissa.be</a>'nin bulunduğu bir önceki sunucu da (Debian 4.0) bir dosya için ayrılması düşünülen dosya indeks boyutu (bytes-per-inode) 4096 ve dosya indeks alanı ise 128 idi. Şuan mevcut sunucumda (Ubuntu 9.10) ise varsayılan kurulum ayarları (8096 / 128) olarak geliyor.</p>

<p>Diskinize ait inode ve block gibi değerleri görmek için;</p>

<blockquote>
	<table class="info">
		<tr>
			<td colspan="2"><p>root@localhost:~#<strong> tune2fs -l /dev/sdc</strong></p></td>
		</tr>
		<tr>
			<th>Inode count:</th>
			<td>1280000</td>
		</tr>
		<tr>
			<th>Free inodes:</th>
			<td>1255224</td>
		</tr>
		<tr>
			<th>Inodes per group:</th>
			<td>32000</td>
		</tr>
		<tr>
			<th>Inode blocks per group:</th>
			<td>1000</td>
		</tr>
		<tr>
			<th>Inode size:</th>
			<td>128</td>
		</tr>
	</table>
</blockquote>

<p>Sorunu tespit ettikten sonra çözüm bulmak gerçekten çok kolay oluyor. Linux'ta kissa.be servisine özel bir disk alanı gerekiyordu. Sunucuda inode değerleri ihtiyacıma göre olan bir alan yaratınca sorun kökten çözüldü. Böylece sunucunun işletim sistemi bu durumdan hiç etkilenmedi. </p>

<p>Diski inode değerlerine göre yeniden biçimlendirirken;</p>

<blockquote>

 root@localhost:~# <strong>mkfs.ext3 -i 4096 -I 128 /dev/sdc</strong>
</blockquote>

<p>Aslında bu konularda uzman biri olduğumu pek söyleyemem. Çok anlamam ama, linux sistemiyle uğraşmayı, sistem programlama konularını seviyorum. </p>

<p>Yazının ana fikrine gelecek olursak;</p>

<p>Eğer kissa.be heveskar bir gencin projesi değil de, bit.ly gibi planlı bir proje olsaydı, gereksinim analizini okuyan bir Sistem Mimari servise ait dosyaları barındıran diskin formatlanması konusunda inode detayını atlamazdı.</p>

<p>Yaşadığım bu olay, bugün öğrendiğim küçük bir ders oldu!...</p>
