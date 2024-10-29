---
title: SQL小節作業：家具店的菜雞銷售奇遇記
date: 2024-10-28 03:10:09
tags: Practice
description: 集合運算
---
謹以本篇記錄小美同學運用入門SQL語法，維運『築夢家居』的事績。

## 資料載入
首先，我們使用這段程式碼創建一個名為products的資料表，並插入一些商品數據。
<font color=#0000FF> ln [1]: </font>

```sql
CREATE TABLE products (
   name VARCHAR(100),         -- 商品名稱
   price INTEGER,            -- 原價
   discount_price INTEGER,    -- 優惠價
   stock INTEGER,            -- 庫存數量
   category VARCHAR(50),      -- 商品分類
   status VARCHAR(20)         -- 商品狀態
);
```
<font color=#FF0000> Out [1]: </font>

![create table](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2F1.png?alt=media&token=af1d0c30-9165-45c0-950e-891d3d0c4d82)
>**CREATE TABLE products：** 這行表示我們正在創建一個名為products的資料表。
>**name VARCHAR(100)：** 這欄位儲存商品名稱，最多可包含100個字元。
>**price INTEGER：** 這欄位儲存商品的原價，以整數形式表示。
>**discount_price INTEGER：** 這欄位儲存商品的優惠價，也是整數。
>**stock INTEGER：** 這欄位表示庫存數量，使用整數。
>**category VARCHAR(50)：** 這欄位表示商品的分類，最多可包含50個字元。
>**status VARCHAR(20)：** 這欄位表示商品的狀態，例如“active”或“inactive”，最多可包含20個字元。

接著使用下列程式碼輸入資料。

<font color=#0000FF>  In [2]: </font>

```sql
INSERT INTO products (name, price, discount_price, stock, category, status) VALUES
   ('北歐風雙人沙發', 39900, 35900, 3, '沙發', 'active'),
   ('貓抓皮L型沙發', 58900, 52900, 1, '沙發', 'active'),
   ('典雅三人座沙發', 42800, 42800, 5, '沙發', 'active'),
   ('工業風電視櫃', 5900, 4900, 12, '櫃子', 'active'),
   ('簡約書櫃', 3500, 3500, 8, '櫃子', 'active'),
   ('玄關鞋櫃', 2900, 2900, 15, '櫃子', 'active'),
   ('日式雙人床架', 12000, 11200, 6, '床架', 'active'),
   ('掀床五尺雙人床', 19900, 18900, 2, '床架', 'active'),
   ('兒童床架', 8900, 8900, 0, '床架', 'inactive'),
   ('電腦辦公椅', 4500, 3900, 20, '椅子', 'active'),
   ('餐椅四入組', 6000, 5200, 8, '椅子', 'active'),
   ('北歐風餐桌', 15800, 14800, 4, '桌子', 'active'),
   ('實木咖啡桌', 3200, 2900, 10, '桌子', 'active'),
   ('電競書桌', 8900, 8900, 0, '桌子', 'inactive');
```
<font color=#FF0000> Out [2]: </font>

![create table data](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2F2.png?alt=media&token=e945cdf0-d7f2-468e-91a5-3245f543c8d7)
>**INSERT INTO products (...) VALUES (...)：**這段語句用於向products表中插入多行數據。
每一行代表一個商品的數據，包括名稱、原價、優惠價、庫存、分類和狀態。

現在我們就可以使用以下SQL查詢，來查看資料庫中products表的所有資料。
<font color=#0000FF>  In [3]: </font>

```sql
SELECT * FROM products;
```

<font color=#FF0000> Out [3]:  </font>

![product databate](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2F3.png?alt=media&token=70b9c983-c836-4e3a-957b-ccad1ff77e23)

## 基礎比較運算：
### 情境 1：單品查詢
#### 客人：「這張北歐風雙人沙發多少錢？」
<font color=#0000FF> In [4]: </font>

```sql
SELECT name, price, discount_price, stock 
FROM products 
WHERE name = '北歐風雙人沙發';
```

<font color=#FF0000> Out [4]: </font>

![where name](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq1.png?alt=media&token=0f69dea2-10ec-493b-ac18-3cef62264953)
>這段查詢的作用是從products表中選擇商品名稱、原價、優惠價和庫存數量，並且條件是商品名稱必須是“北歐風雙人沙發”。

## 情境 2：價格比較
### 客人：「請列出 5000 元以下的櫃子有哪些？」
<font color=#0000FF> In [5]: </font>

```sql
SELECT name, price, discount_price, stock 
FROM products 
WHERE category = '櫃子' AND price < 5000;
```

<font color=#FF0000> Out [5]: </font>

![where and](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq2.png?alt=media&token=7a8f69c1-79cc-4744-8c3e-94de0721fe0f)
>這段查詢會從products表中選擇商品名稱、原價、優惠價和庫存數量，並且條件是商品分類為“櫃子”且原價低於5000。

## 情境 3：庫存確認
### 客人：「日式雙人床架還有貨嗎？」
<font color=#0000FF> In [6]: </font>

```sql
SELECT stock 
FROM products 
WHERE name = '日式雙人床架';
```

<font color=#FF0000>  Out [6]: </font>

![where](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq3.png?alt=media&token=a1074bad-6f29-4b10-ab0c-672169bc51bd)
>這段查詢會從products表中選擇“日式雙人床架”的庫存數量。如圖所示，剩下6個。

## 邏輯運算 AND：
### 情境 4：預算內的商品
#### 客人：「想找 4 萬以下，而且有現貨的沙發」
<font color=#0000FF> In [7]: </font>

```sql
SELECT name, price, discount_price, stock 
FROM products 
WHERE category = '沙發' AND price < 40000 AND stock > 0;
```

<font color=#FF0000>  Out [7]: </font>

![where and and ](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq4.png?alt=media&token=ecb72dfb-4872-4197-af8c-6428663c4444)
>這段查詢會從products表中選擇商品名稱、原價、優惠價和庫存數量，並且條件是商品分類為“沙發”、原價低於40,000以及庫存數量大於0。

### 情境 5：特價且有貨
#### 客人：「沙發有哪些特價且現貨的品項？」
<font color=#0000FF> In [8]: </font>

```sql
SELECT name, price, discount_price, stock 
FROM products 
WHERE category = '沙發' AND price > discount_price AND stock > 0;
```

<font color=#FF0000>  Out [8]: </font>

![where and and ](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq5.png?alt=media&token=4cd4560b-a2bd-437e-90f9-c31ee94b4bc5)
>這段查詢會從products表中選擇商品名稱、原價、優惠價和庫存數量，並且條件是商品分類為“沙發”、原價大於優惠價（表示特價）以及庫存數量大於0。

## 邏輯運算 OR：
### 情境 6：多分類查詢
#### 客人：「我要找櫃子或桌子」
<font color=#0000FF> In [9]: </font>

```sql
SELECT name, price, discount_price, stock 
FROM products 
WHERE category = '櫃子' OR category = '桌子';
```

<font color=#FF0000> Out [9]: </font>

![where or](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq6.png?alt=media&token=844a66fa-1da7-4b52-a0a7-d15544827154)
>這段查詢會從products表中選擇商品名稱、原價、優惠價和庫存數量，並且條件是商品分類為“櫃子”或“桌子”。這樣就能找到所有符合這些分類的商品。

### 情境 7：指定商品
#### 客人：「北歐風雙人沙發和貓抓皮L型沙發哪個還有貨？」
<font color=#0000FF> In [10]: </font>

```sql
SELECT name, stock 
FROM products 
WHERE name IN ('北歐風雙人沙發', '貓抓皮L型沙發') AND stock > 0;
```

<font color=#FF0000> Out [10]: </font>

![where namee in and](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq7.png?alt=media&token=27062c29-0cab-48df-ab02-3679642e3000)
>這段查詢會從products表中選擇商品名稱和庫存數量，條件是商品名稱是“北歐風雙人沙發”或“貓抓皮L型沙發”，並且庫存數量大於0。這樣就能從兩個商品中，選出還有庫存的商品。

## IN 運算：
### 情境 8：多分類查詢
#### 客人：「客廳的家具有哪些？我要看沙發、櫃子跟桌子」
<font color=#0000FF> In [11]: </font>

```sql
SELECT name, category, price, discount_price, stock 
FROM products 
WHERE category IN ('沙發', '櫃子', '桌子');
```

<font color=#FF0000> Out [11]: </font>

![where in](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq8.png?alt=media&token=8e7c483e-c531-408f-9dcb-50d95086c21b)
>這段查詢會從products表中選擇商品名稱、分類、原價、優惠價和庫存數量，條件是商品分類為“沙發”、“櫃子”或“桌子”。這樣就能找到所有屬於這三種類別的產品。

## 情境 9：特定商品
### 客人：「電腦辦公椅和餐椅四入組的價格是多少？」
<font color=#0000FF> In [12]: </font>

```sql
SELECT name, price, discount_price 
FROM products 
WHERE name IN ('電腦辦公椅', '餐椅四入組');
```

<font color=#FF0000>  Out [12]: </font>

![where name in](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq9.png?alt=media&token=4a409e6d-0a66-431e-b0df-0b7bb3a4c9a0)
>這段查詢會從products表中選擇商品名稱、原價和優惠價，條件是商品名稱是“電腦辦公椅”或“餐椅四入組”

## BETWEEN：
### 情境 10：價格區間
#### 客人：「想找 10000 到 20000 之間的商品有哪些？」
<font color=#0000FF>  In [13]: </font>

```sql
SELECT name, price, discount_price, stock 
FROM products 
WHERE price BETWEEN 10000 AND 20000;
```

<font color=#FF0000>  Out [13]: </font>

![where between and](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq10.png?alt=media&token=8e417fca-c3f1-415f-9b60-28a61cd8b8df)
>這段查詢會從products表中選擇商品名稱、原價、優惠價和庫存數量，條件是商品的價格在10,000到20,000之間。

### 情境 11：庫存區間
#### 主管：「請列出庫存在 5 到 15 之間的商品」
<font color=#0000FF>  In [14]: </font>

```sql
SELECT name, category, price, discount_price, stock 
FROM products 
WHERE stock BETWEEN 5 AND 15;
```

<font color=#FF0000>  Out [14]: </font>

![where between and](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq11.png?alt=media&token=ea97af73-0475-4491-9470-e45fe1ce0eeb)
>這段查詢會從products表中選擇商品名稱、分類、原價、優惠價和庫存數量，條件是商品的庫存數量在5到15之間。

## NOT IN：
### 情境 12：排除商品
#### 主管：「列出除了沙發和床架以外的商品」
<font color=#0000FF>  In [15]: </font>

```sql
SELECT name, category, price, discount_price, stock 
FROM products 
WHERE category NOT IN ('沙發', '床架');
```

<font color=#FF0000> Out [15]: </font>

![where not in](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq12.png?alt=media&token=76b87bab-1983-4fe1-9899-9bca9e822d7b)
>這段查詢會從products表中選擇商品名稱、分類、原價、優惠價和庫存數量，條件是商品的分類不屬於“沙發”或“床架”。

## 更新和刪除：
### 情境 13：調整價格
#### 主管：「北歐風雙人沙發要調降 2000 元」
<font color=#0000FF>  In [16]: </font>

```sql
UPDATE products 
SET price = price - 2000 
WHERE name = '北歐風雙人沙發';
```

<font color=#FF0000>  Out [16]: </font>

![update set price where name](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq13.png?alt=media&token=7190057c-28f6-44d3-b685-8c38a86e63b7)

![updated table](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq13-table.png?alt=media&token=0d709478-d812-4b95-ae96-4fa4abc074f5)
>這段查詢會更新products表中“北歐風雙人沙發”的價格，將其現有價格減去2,000元。
>更新後查詢「北歐風雙人沙發」price 應如上圖所示。

## 情境 14：更新庫存
### 主管：「電腦辦公椅進了 5 張」

<font color=#FF0000> In [17]: </font>

```sql
UPDATE products 
SET stock = stock + 5 
WHERE name = '電腦辦公椅';
```
<font color=#FF0000> Out [17]: </font>

![update set stock where name](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq13.png?alt=media&token=7190057c-28f6-44d3-b685-8c38a86e63b7)

![update table](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq14-table.png?alt=media&token=a259eff6-6bc7-46a5-8a34-c39b946b0b92)
>這段查詢會更新products表中“電腦辦公椅”的庫存數量，將其現有庫存增加5張。
>更新後查詢「電腦辦公椅」stock 應如上圖所示。


### 情境 15：清除資料
#### 主管：「要清掉兒童床架和電競書桌的資料」
<font color=#FF0000>In [18]: </font>

```sql
DELETE FROM products 
WHERE name IN ('兒童床架', '電競書桌');
```

<font color=#FF0000> Out [18]: </font>

![delete](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq15.png?alt=media&token=8f71e060-3dfb-4f92-b060-f7fdfa9755b3)

![delete](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E5%AE%B6%E5%85%B7%E5%BA%97%E7%9A%84%E8%8F%9C%E9%9B%9E%E9%8A%B7%E5%94%AE%E5%A5%87%E9%81%87%E8%A8%98%2Fq15-table.png?alt=media&token=89285b10-ebb6-43c2-a416-fc85c9e759bd)
>這段查詢會從products表中刪除商品名稱為“兒童床架”和“電競書桌”的所有資料。 
>更新後的資料庫應如上圖所示。

## 回顧： 本次練習常用語法
<font color=#FF6600>SELECT</font> column_name 
<font color=#FF6600>FROM</font> table_name
>>SELECT與FROM 敘述是從指定的資料表中選擇欄位的查詢語法，查詢結果依據其存在資料表中的順序所呈現。

<font color=#FF6600>WHERE</font> condirion
>>WHERE 敘述能以「條件」作為篩選觀測值的依據。

如果沒有問題的話，那我們就可以前往下一章節囉。d(d＇∀＇)