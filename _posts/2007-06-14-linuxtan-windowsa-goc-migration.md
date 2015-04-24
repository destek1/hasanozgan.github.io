---
layout: post
title: Linux'tan, Windows'a Göç (Migration) !
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Aman yanlış anlaşılmasın! Linux'tan Windows'a göç etmek bence aptallıktır!. PHP ile yazılmış bir projeyi Linux'tan Windows'a göç ettirmek için şirketten bir iş atandı üzerime. PHP ile yazılmış olan Web uygulamasını göç ettirirken kodda sadece LDAP ile ilgili bazı değişiklikler yaptım. Tahmin edeceğiniz gibi Web için bu değişiklik bile fazla. Asıl değişiklik Cron'da çalışan bir kabul betiği (shell script) idi ki, bunu yeniden; yazarken Windows betiğine dair yeni şeyler öğrendim. Shell scriptin yaptığı Samba protokolünden ağ üzerindeki bir makinayi mount ediyor ve mount edilen dizinlerdeki dosyalar üzerinde işlem yapıyordu. İşte bu işlemin Windowsta ki karşılığı olan <strong>"Mapping Network Drive"</strong> işlemini yaparak sanal bir sürücü oluşturmam gerekiyordu. Windows'ta bu işin <strong>net</strong> komutu ile yapıldığını tahmin ediyordum. Bakın şu Allah'ın işine! <a href="http://www.cae.wisc.edu/site/public/?title=nt4netuse">Haklıymışım</a> !

<strong>Linux'ta yapılan;</strong>

<em>mount -t smbfs -o username=admin,password=adminpass,workgroup=stargate //machine_name/documents /mnt/documents/</em>

<strong>yada</strong>

<em>mount -t cifs //10.100.8.36/documents /mnt/documents/ -o username=admin,password=adminpass</em>

<strong>Windows'ta yapılması gereken;</strong>

<em>net use h: \\machine_name\documents</em>
