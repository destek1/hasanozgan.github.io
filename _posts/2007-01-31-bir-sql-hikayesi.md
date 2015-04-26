---
layout: post
title: Bir SQL Hikayesi
tags:
- Diğer
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Bazen MS-SQL kullandığımı unutup, MySQL'deki gibi sorgular yazıyorum. Geçen zaman diliminde geliştirdiğim bir projenin DB yapısında bazı refactoring işlemleri yaptıktan sonra; göç (migration) için gerekli olan SQL betiklerini(script) yazdım. Tabii alışkanlıktan aşağıdaki gibi bir betik hazırladım.
<p style="padding-left: 50px"><span style="color: #0000ff;">UPDATE </span>
<span style="color: #000000;">Bid b, </span>
<span style="color: #0000ff;">Product </span>
<span style="color: #000000;">p </span>
<span style="color: #0000ff;">SET </span>
<span style="color: #000000;">p.CategoryId=b.CategoryId </span>

<span style="color: #0000ff;">WHERE </span>
<span style="color: #000000;">b.ProductId = p.Id;</span>

Daha sonra, yazdığım göç betiklerini test ederken gördüm ki, MSSQL bu işlemi desteklemiyor. Böyle bir işlemi yapabilmek için T-SQL yazmak gerekiyor. Sonrada aşağıda gördüğünüz kodu yazdım.

Buraya da yazayım dedim; belki birinin T-SQL'de CURSOR örneğine ihtiyacı olur yada yukarıdaki gibi MySQL'de ki gibi MSSQL'de Multiple Update işlemi yapmak ister :-)
<p style="padding-left:50px"><span style="color: #0000ff;">DECLARE </span>
cr_BidCategoryToProductCategory
<span style="color: #0000ff;">CURSOR FOR </span>

<span style="color: #0000ff;">SELECT DISTINCT </span>
p.Id, b.CategoryId
<span style="color: #0000ff;">FROM </span>
Bid b,
<span style="color: #0000ff;">Product </span>p

<span style="color: #0000ff;">WHERE </span>
b.ProductId = p.Id;

<span style="color: #0000ff;">DECLARE </span>@productId
<span style="color: #0000ff;">int</span>, @categoryId
<span style="color: #0000ff;">int</span>;

<span style="color: #0000ff;">OPEN </span>
cr_BidCategoryToProductCategory;

<span style="color: #0000ff;">FETCH </span>
cr_BidCategoryToProductCategory
<span style="color: #0000ff;">INTO </span>@productId, @categoryId

<span style="color: #0000ff;">WHILE </span>(@@FETCH_STATUS = 0)

<span style="color: #0000ff;">BEGIN
</span>
<span style="color: #0000ff;">UPDATE Product SET </span>
CategoryId = @categoryId
<span style="color: #0000ff;">WHERE </span>Id = @productId;

<p style="padding-left:50px"><span style="color: #0000ff;">FETCH </span>
cr_BidCategoryToProductCategory
<span style="color: #0000ff;">INTO </span>
@productId, @categoryId

<span style="color: #0000ff;">END
CLOSE </span>
cr_BidCategoryToProductCategory;

<span style="color: #0000ff;">DEALLOCATE </span>
cr_BidCategoryToProductCategory;
