---
title: SQL小節練習：晴天咖啡廳
date: 2024-11-21 23:54:43
tags: Practice
description: ㄖㄨㄟㄙㄡㄙㄡㄒ一ㄉㄛㄒ一ㄌㄚㄙㄡㄌㄚㄒ一ㄒ一ㄒ一ㄒ一ㄌㄚㄒ一ㄌㄚㄙㄡ
---
## 資料載入
[線上資料庫操作網站 PG-SQL:Temporary Postgres Database.]( post-sql.com)

將資料倒入 pg-sql

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

INSERT INTO products (name, price, discount_price, stock, category, status) VALUES
    ('精品手沖咖啡', 180, 160, 50, '咖啡', 'active'),
    ('美式咖啡', 120, 120, 100, '咖啡', 'active'),
    ('摩卡咖啡', 150, 150, 80, '咖啡', 'active'),
    ('特調拿鐵', 160, 140, 60, '咖啡', 'active'),
    ('伯爵紅茶', 100, 100, 70, '茶飲', 'active'),
    ('玫瑰花茶', 120, 120, 30, '茶飲', 'active'),
    ('柳橙汁', 90, 80, 40, '果汁', 'active'),
    ('水果茶', 130, 110, 45, '茶飲', 'active'),
    ('提拉米蘇', 160, 160, 15, '甜點', 'active'),
    ('草莓乳酪蛋糕', 180, 150, 8, '甜點', 'active'),
    ('巧克力布朗尼', 150, 150, 0, '甜點', 'inactive'),
    ('特選咖啡豆', 500, 450, 20, '咖啡豆', 'active'),
    ('摩卡咖啡豆', 480, 480, 15, '咖啡豆', 'active'),
    ('濾掛式咖啡包', 25, 20, 200, '咖啡', 'active'),
    ('手沖濾紙', 180, 180, 30, '器材', 'active');
```

<font color=#0000FF>  In [2]: </font>

```sql
SELECT * FROM products;
```

<font color=#FF0000> Out [2]:  </font>

![coffeeShopProduct](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2F1.png?alt=media&token=2c1b49c7-ed1a-4583-904f-4d4bfb813c1e)

>創建了一個名為 products 的資料表，該表用來存儲商品的詳細信息。
>>**name：**商品名稱，類型為 VARCHAR(100)，用來存儲商品的名稱。
>>**price：**原價，類型為 INTEGER，用來存儲商品的原始價格。
>>**discount_price：**優惠價，類型為 INTEGER，用來存儲商品的折扣後價格。
>>**stock：**庫存數量，類型為 INTEGER，用來存儲商品的庫存數量。
>>**category：**商品分類，類型為 VARCHAR(50)，用來存儲商品的分類，例如「咖啡」、「茶飲」等。
>>**status：**商品狀態，類型為 VARCHAR(20)，用來存儲商品的狀態，例如「active」（可售）或「inactive」（不可售）。





## 基礎查詢篇：
### 情境 1：缺貨確認
顧客：「草莓乳酪蛋糕還有嗎？」
小杰想查：要確認草莓乳酪蛋糕的庫存

<font color=#0000FF>  In [3]: </font>

```sql
SELECT stock FROM products WHERE name = '草莓乳酪蛋糕';
```

<font color=#FF0000> Out [3]:  </font>
![q1](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq1.png?alt=media&token=e3852780-01f6-43c4-b1f7-57345b7c14ee)

>返回「草莓乳酪蛋糕」的庫存數量。根據最初倒入的數據，「草莓乳酪蛋糕」的庫存數量應該是8。

## 情境 2：優惠查詢
顧客：「有什麼特價的咖啡嗎？」
小杰想查：列出所有有特價（優惠價低於原價）的咖啡類商品

<font color=#0000FF>  In [4]: </font>

```sql
SELECT * FROM products 
WHERE category = '咖啡' AND discount_price < price;
```
<font color=#FF0000> Out [4]:  </font>
![q2](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq2.png?alt=media&token=cc0d3abf-6d9f-4015-b607-c8069060ae85)

>從 products 表中選出所有分類為「咖啡」且優惠價低於原價的商品。
>這樣就可以找到目前正在促銷的咖啡類商品。

## 情境 3：價格區間
顧客：「有沒有100元以下的飲品？」
小杰想查：找出所有100元以下的飲品

<font color=#0000FF>  In [5]: </font>

```sql
SELECT * FROM products 
WHERE category IN ('咖啡', '茶飲', '果汁') AND discount_price < 100;
```

<font color=#FF0000> Out [5]:  </font>
![q3](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq3.png?alt=media&token=dd7ebec2-8fc0-4cdf-9c6f-a3e71544d915)

>選擇所有分類為「咖啡」、「茶飲」或「果汁」且優惠價低於100元的商品。
>這樣就可以找到所有符合條件的飲品。

## AND條件篇
### 情境 4：庫存與價格
顧客：「有沒有特價，而且還有貨的甜點？」
小杰想查：要同時符合有特價（優惠價<原價）且還有庫存的甜點

<font color=#0000FF>  In [6]: </font>

```sql
SELECT * FROM products 
WHERE category = '甜點' AND discount_price < price AND stock > 0;
```

<font color=#FF0000> Out [6]:  </font>
![q4](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq4.png?alt=media&token=5bab43d9-c1fa-40a7-86cf-0c880a22663a)

>從 products 表中選出所有分類為「甜點」、優惠價低於原價且庫存量大於0的商品。
>這樣可以找出目前有特價並且還有庫存的甜點。

## 情境 5：價格與分類
店長：「幫我查一下所有200元以上，而且還有庫存的咖啡類商品」
小杰想查：列出符合價格和分類條件的商品

<font color=#0000FF>  In [7]: </font>

```sql
SELECT * FROM products 
WHERE category = '咖啡' AND price > 200 AND stock > 0;
```
<font color=#FF0000> Out [7]:  </font>
![q5](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq5.png?alt=media&token=42bdbb1a-84e6-4efd-af7a-3c431356417c)
>從 products 表中選出所有分類為「咖啡」、原價超過200元且庫存量大於0的商品。

## OR條件篇
### 情境 6：多分類查詢
顧客：「我想看看你們的咖啡豆和濾掛包」
小杰想查：列出咖啡豆類和濾掛式咖啡的商品

<font color=#0000FF>  In [8]: </font>

```sql
SELECT * FROM products 
WHERE category = '咖啡豆' OR name = '濾掛式咖啡包';
```

<font color=#FF0000> Out [8]:  </font>
![q6](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq6.png?alt=media&token=e762f084-686d-4551-8165-45dd5e868014)

>從 products 表中選出所有分類為「咖啡豆」的商品以及名稱為「濾掛式咖啡包」的商品。

## BETWEEN篇
### 情境 7：價格區間
顧客：「想找100到200元之間的飲品」
小杰想查：列出這個價格區間的飲品

<font color=#0000FF>  In [9]: </font>

```sql
SELECT * FROM products 
WHERE category IN ('咖啡', '茶飲', '果汁') AND discount_price BETWEEN 100 AND 200;
```

<font color=#FF0000> Out [9]:  </font>
![q7](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq7.png?alt=media&token=d6133a03-1f4b-4916-99aa-6983a7d59d72)

>從 products 表中選出所有分類為「咖啡」、「茶飲」或「果汁」，且優惠價在100到200元之間的商品。

## 更新資料篇
### 情境 8：調整價格
店長：「美式咖啡要降價10元」
小杰想查：如何更新美式咖啡的優惠價

<font color=#0000FF>  In [10]: </font>

```sql
UPDATE products 
SET discount_price = discount_price - 10 
WHERE name = '美式咖啡';
```

<font color=#FF0000> Out [10]:  </font>
![q8](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq8-result.png?alt=media&token=9a462bdb-86de-4f74-8b0f-018bb078e4f6)

<font color=#0000FF>  In [11]: </font>

```sql
SELECT name, price, discount_price
FROM products
WHERE name = '特調拿鐵';
```

<font color=#FF0000> Out [11]:  </font>
![q8Table](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq8-.png?alt=media&token=78170701-c53f-4412-961c-f3f9677433e4)

>將 products 表中名稱為「美式咖啡」的商品的優惠價降低10元。

### 情境 9：更新庫存
店長：「特選咖啡豆進了10包」
小杰想查：如何增加特選咖啡豆的庫存

<font color=#0000FF>  In [12]: </font>

```sql
UPDATE products 
SET discount_price = discount_price - 10 
WHERE name = '美式咖啡';

```

<font color=#FF0000> Out [12]:  </font>
![q9](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq8-result.png?alt=media&token=9a462bdb-86de-4f74-8b0f-018bb078e4f6)

<font color=#0000FF>  In [13]: </font>

```sql
SELECT name, stock
FROM products
WHERE name = '特選咖啡豆';
```

<font color=#FF0000> Out [13]:  </font>
![q9Table](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E7%B7%B4%E7%BF%92%EF%BC%9A%E3%80%8C%E6%99%B4%E5%A4%A9%E5%92%96%E5%95%A1%E5%BB%B3%E3%80%8D%2Fq9-.png?alt=media&token=7e39fd68-fbca-44d9-b3f7-14aa799773b5)

>將 products 表中名稱為「特選咖啡豆」的商品的庫存增加10包。

<font color=#c0c0c0> 吹著前奏望著天空 我想起花瓣試著掉落 </font>