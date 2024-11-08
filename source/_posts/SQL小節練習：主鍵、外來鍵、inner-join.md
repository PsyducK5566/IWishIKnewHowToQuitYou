---
title: SQL小節練習：主鍵、外來鍵、inner join
date: 2024-11-05 21:44:34
tags: Practice
description:   AIRBORNE   >口< ✊
---

[課堂簡報連結](https://gamma.app/docs/SQL--23heyix4r93u5u0?mode=doc)
[線上資料庫操作網站 PG-SQL:Temporary Postgres Database.]( https://pg-sql.com/)

## Q1：拯救明華國小的資料庫，哪個欄位適合變成**外來鍵**？

<table>
  <tr>
    <th>學生編號</th>
    <th>姓名</th>
    <th>班級</th>
    <th>性別</th>
    <th>年齡</th>
  </tr>
  <tr>
    <td>1</td>
    <td>小明</td>
    <td>三年一班</td>
    <td>男</td>
    <td>8</td>
  </tr>
  <tr>
    <td>2</td>
    <td>小華</td>
    <td>三年二班</td>
    <td>女</td>
    <td>9</td>
  </tr>
  <tr>
    <td>3</td>
    <td>小美</td>
    <td>三年一班</td>
    <td>男</td>
    <td>8</td>
  </tr>
  <tr>
    <td>4</td>
    <td>小強</td>
    <td>三年一班</td>
    <td>女</td>
    <td>8</td>
  </tr>
   <tr>
    <td>5</td>
    <td>小智</td>
    <td>三年二班</td>
    <td>男</td>
    <td>9</td>
  </tr>
</table>

班級。因為班級與學生呈現**一對多**的關係，所以應該把班級拆成學生外來鍵。
>**班級的獨特性：**每個班級會有一個獨特的名稱或編號，用於標識不同的班級。
>**關聯性：**班級可以用來連接到一個包含班級詳細資訊的表，這樣可以實現資料的關聯性。

創建班級資料表
<font color=#0000FF> In [1]: </font>

```sql
CREATE TABLE class_list (
    id SERIAL PRIMARY KEY, --自動生成的唯一識別碼（使用 SERIAL 型別，會自動遞增），作為每個班級的主鍵（PRIMARY KEY）
    name VARCHAR(50) 
);
```
<font color=#FF0000> Out [1]: </font>
![creat table result](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F1-1%262%E5%BB%BA%E7%AB%8B%E8%B3%87%E6%96%99%E8%A1%A8%E6%A0%BC%E5%BC%8F.png?alt=media&token=b97fc110-7fb1-434b-9bee-02926e59d793)


創建學生資料表
<font color=#0000FFF> In [2]: </font>

```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY, --自動生成的唯一識別碼，作為每個學生的主鍵。
    name VARCHAR(50),
    gender VARCHAR(10), --這是一個整數欄位，用來儲存學生的性別識別碼，參照 gender_list 表格中的 id 欄位。
    age INTEGER,
    class_id INTEGER, --這是一個整數欄位（INTEGER），用來儲存學生所屬班級的識別碼，並且是參照 class_list 表格中的 id 欄位（這是一個外鍵關係，確保學生所屬的班級在 class_list 中是存在的）。
    FOREIGN KEY (class_id) REFERENCES class_list(id) -- 設定外來鍵關聯。
);
```
<font color=#FF0000> Out [2]: </font>
![creat table result](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F1-1%262%E5%BB%BA%E7%AB%8B%E8%B3%87%E6%96%99%E8%A1%A8%E6%A0%BC%E5%BC%8F.png?alt=media&token=b97fc110-7fb1-434b-9bee-02926e59d793)

新增班級資料
<font color=#0000FF> In [3]: </font>

```sql
INSERT INTO class_list (name) VALUES --這部分表示要向class_list表中插入數據，並指定插入的欄位是name
    ('三年一班'),
    ('三年二班');
```
<font color=#FF0000> Out [3]: </font>
![INSERT INTO result](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F1-3%20%E8%BC%B8%E5%85%A5%E6%95%B8%E6%93%9A.png?alt=media&token=05638155-7ae4-4eff-b190-6370b8ae3345)


新增學生資料
<font color=#0000FF> In [4]: </font>

```sql
INSERT INTO students (name, age, gender, class_id) VALUES
    ('小明', 8, '男', 1),
    ('小華', 9, '女', 2),
    ('小美', 8, '男', 1),
    ('小強', 8, '女', 1),
    ('小智', 9, '男', 2);
```
>這些數據將被插入到students表中，每個學生都有一個自動生成的唯一id。class_id欄位用於指明學生所屬的班級，並且應該對應於class_list表中已存在的班級id，以維持數據的完整性和關聯性。

<font color=#FF0000> Out [4]: </font>
![ISERT INTO result](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F1-4%20%E8%BC%B8%E5%85%A5%E6%95%B8%E6%93%9A.png?alt=media&token=54ae6917-925d-4725-9133-adf8220e5fbb)

顯示數據
<font color=#0000FF> In [5]: </font>

```sql
SELECT 
    students.id AS 學生編號,
    students.name AS 姓名,
    class_list.name AS 班級,
    students.gender AS 性別,
    students.age AS 年齡    
FROM students
INNER JOIN class_list ON students.class_id = class_list.id;
```
>這個查詢會返回一個結果集，其中包含每個學生的編號、姓名、班級名稱、性別和年齡。這樣的查詢有助於獲取完整的學生和班級資訊，便於查看和分析。

<font color=#FF0000> Out [5]: </font>
![SELECT FROM Students](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F1-5%20%E9%A1%AF%E7%A4%BA%E6%95%B8%E6%93%9A.png?alt=media&token=3efb6f21-603e-4c91-84c6-8a1a71ee6d70)

## Q2：第一題的延伸，多了一個*班級老師*

<table>
  <tr>
    <th>學生編號</th>
    <th>姓名</th>
    <th>班級</th>
    <th>班級老師</th>
    <th>性別</th>
    <th>年齡</th>
  </tr>
  <tr>
    <td>1</td>
    <td>小明</td>
    <td>三年一班</td>
    <td>廖洧杰</td>
    <td>男</td>
    <td>8</td>
  </tr>
  <tr>
    <td>2</td>
    <td>小華</td>
    <td>三年二班</td>
    <td>卡期伯</td>
    <td>女</td>
    <td>9</td>
  </tr>
  <tr>
    <td>3</td>
    <td>小美</td>
    <td>三年一班</td>
    <td>查理</td>
    <td>男</td>
    <td>8</td>
  </tr>
  <tr>
    <td>4</td>
    <td>小強</td>
    <td>三年一班</td>
    <td>麥可</td>
    <td>女</td>
    <td>8</td>
  </tr>
   <tr>
    <td>5</td>
    <td>小智</td>
    <td>三年二班</td>
    <td>李燕容</td>
    <td>男</td>
    <td>9</td>
  </tr>
</table>

在設計資料庫時，是否將班級導師設為外來鍵取決於你的數據關聯需求。以下是一些考量：
#### 使用外來鍵的情況
##### 導師有獨立的表格：
如果導師有自己的表格（例如teachers表），並且你需要存儲導師的詳細資訊（如聯絡方式、專業等），那麼將teacher_id設為外來鍵是合適的。
##### 數據一致性：
使用外來鍵可以確保數據的完整性和一致性，防止班級中出現不存在的導師。
#### 不使用外來鍵的情況
##### 簡單的系統：
如果系統相對簡單，且導師資訊不需要獨立管理，可以直接在class_list表中使用teacher名稱欄位。
##### 靈活性：
不使用外來鍵可以增加靈活性，尤其是在導師變動頻繁或不需要嚴格關聯的情況下。


從表中可以觀察班級與班級老師呈現**一對多**關係(六角幼兒園?)，學生與老師則是**一對一**關係；故在此我們把老師資料拆成學生的外來鍵。

創建班級老師資料表
<font color=#0000FF> In [6]: </font>

```sql
CREATE TABLE teachers (
    id SERIAL PRIMARY KEY,     -- 老師編號，主鍵
    name VARCHAR(50)           -- 老師名稱
);
```
>id是這個表的第一個欄位，用來存儲老師的編號。
>SERIAL是一個數據類型，表示這個欄位會自動生成遞增的整數值，通常用於主鍵。
>PRIMARY KEY表示這個欄位是主鍵，每個值必須是唯一的，這樣可以唯一標識每一位老師。

<font color=#FF0000> Out [6]: </font>
![CREAT TABLE teachers](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F2-1.png?alt=media&token=d79c3f30-07f8-4d7a-8554-05903932e24e)

新增老師資料
<font color=#0000FF> In [7]: </font>

```sql
INSERT INTO teachers (name) VALUES --向teachers表的name欄位中插入數據。
    ('廖洧杰'),
    ('卡斯伯'),
    ('查理'),
    ('麥可'),
    ('李燕容');
```
<font color=#FF0000> Out [7]: </font>
![INSERT INTO teachers](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F2-2.png?alt=media&token=f105bb3f-2aa1-406c-9611-32962d2758ff)

將學生資料表新增班級老師欄位(teacher_id)
<font color=#0000FF> In [8]: </font>

```sql
ALTER TABLE students --表示要對students表進行修改。
ADD COLUMN teacher_id INTEGER,
ADD CONSTRAINT fk_teacher_id --這個約束確保teacher_id欄位中的值必須存在於teachers表的id欄位中，從而建立學生與老師之間的關聯。
FOREIGN KEY (teacher_id) REFERENCES teachers(id);
```
>ADD COLUMN 用來添加一個新的欄位到表中。
>teacher_id 是新欄位的名稱，用來存儲對應老師的編號。
>FOREIGN KEY 用來定義一個外來鍵約束。
>(teacher_id) 表示這個外來鍵約束作用的欄位是teacher_id。
>REFERENCES teachers(id)表示teacher_id 引用的是teachers表中的id欄位。

<font color=#FF0000> Out [8]: </font>
![ALTER TABLE](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F2-3.png?alt=media&token=2b85b771-6e79-484b-8116-e41925b38d12)

>ALTER 是 SQL 中的語法，用來修改已存在的資料表
>執行這段指令並無任何提示語出現

這樣設計的好處是可以在students表中直接關聯到teachers表中的一位老師，這樣的關聯有助於保持數據的一致性。
例如，如果一個學生有一位指定的老師，您可以通過teacher_id來確保這個關聯是正確的，並且可以方便地查詢每個學生的導師資訊。

更新學生資料表
<font color=#0000FF> In [9]: </font>

```sql
UPDATE students SET teacher_id = 1 WHERE id = 1;
UPDATE students SET teacher_id = 2 WHERE id = 2;
UPDATE students SET teacher_id = 3 WHERE id = 3;
UPDATE students SET teacher_id = 4 WHERE id = 4;
UPDATE students SET teacher_id = 5 WHERE id = 5;
```
>更新students表中的teacher_id欄位，為每個學生分配一位老師。

<font color=#FF0000> Out [9]: </font>
![UPDATE SET WHERE](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F2-4.png?alt=media&token=8669f45b-4b84-495c-ba53-4973b45ff3e5)

這些更新操作將每個學生與一位特定的老師關聯起來，這樣可以在數據庫中方便地查詢和管理學生與老師之間的關係。

使用INNER JOIN 合併資料表查詢學生與班級導師的詳細資料
<font color=#0000FF> In [10]: </font>

```sql
SELECT 
    students.id AS 學生編號,
    students.name AS 姓名,
    class_list.name AS 班級,
    teachers.name AS 班級老師,
    students.gender AS 性別,
    students.age AS 年齡    
FROM students
INNER JOIN class_list ON students.class_id = class_list.id
INNER JOIN teachers ON students.teacher_id = teachers.id
```
>INNER JOIN 用於將{ }表與{ }表連接起來
>ON students.class_id = class_list.id表示連接的條件是students表中的class_id欄位與class_list表中的id欄位相等。
>ON students.teacher_id = teachers.id表示連接的條件是students表中的teacher_id欄位與teachers表中的id欄位相等。

<font color=#FF0000> Out [10]: </font>
![SELECT FORM INNER JOIN ON](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F2-5.png?alt=media&token=59b20324-037e-4354-b7b3-6ced5373fe96)

## Q3：小孩的家庭歸類資料庫，父母資料一直重複實在討厭！

<table>
  <tr>
    <th>小孩編號</th>
    <th>姓名</th>
    <th>父母名稱</th>
    <th>父母電話</th>
    <th>父母性別</th>
  </tr>
  <tr>
    <td>1</td>
    <td>小明</td>
    <td>王大祥</td>
    <td>0973254254</td>
    <td>男</td>    
  </tr> 
  <tr>
    <td>2</td>
    <td>小華</td>
    <td>王曉如</td>
    <td>0955717855</td>
    <td>女</td>    
  </tr> 
  <tr>
    <td>3</td>
    <td>小美</td>
    <td>王大祥</td>
    <td>0973254254</td>
    <td>男</td>    
  </tr> 
  <tr>
    <td>4</td>
    <td>小強</td>
    <td>王曉如</td>
    <td>0955717855</td>
    <td>女</td>    
  </tr>
    <tr>
    <td>5</td>
    <td>小智</td>
    <td>王大祥</td>
    <td>0973254254</td>
    <td>男</td>    
  </tr>
</table>

重複的父母資料可以通過將父母信息獨立出來，建立一個單獨的父母資料表來解決。
然後使用關聯鍵（如父母ID）將小孩表和父母表關聯起來。這樣可以減少數據冗餘，並提高數據庫的可維護性和一致性。

創建父母資料表
<font color=#0000FF> In [11]: </font>

```SQL
CREATE TABLE parents (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    phone VARCHAR(15),
    gender VARCHAR(10)    
);
```

<font color=#FF0000> Out [11]: </font>
![CREATE TABLE parents](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F3-1.png?alt=media&token=92233014-31b6-4909-a7d2-2b8a9757f671)

新增父母資料
<font color=#0000FF> In [12]: </font>

```sql
INSERT INTO parents(name, phone, gender)
VALUES
    ('王大祥', '0973254254', '男'),
    ('王曉如', '0955717855', '女');
```

<font color=#FF0000> Out [12]: </font>
![INSERT INTO parents](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F3-2.png?alt=media&token=78ddfb65-0edc-4430-b4aa-6b49da0fa02f)

新增學生資料表的父母欄位(parent_id)
<font color=#0000FF> In [13]: </font>

```sql
ALTER TABLE students
ADD COLUMN parent_id INTEGER,
ADD CONSTRAINT fk_parent_id
FOREIGN KEY (parent_id) REFERENCES parents(id);
```

<font color=#FF0000> Out [13]: </font>
![INSERT INTO parents](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F3-3.png?alt=media&token=6a66594e-638d-4ac8-aa0a-16c680b20cca)

更新學生資料表， 新增父母資料
<font color=#0000FF> In [14]: </font>

```sql 
UPDATE students 
SET parent_id = 1
WHERE id IN (1, 3, 5); -- 設定 id 為 1,3,5 學生的 parent_id = 1 (王大祥)
UPDATE students 
SET parent_id = 2
WHERE id IN (2, 4); -- 設定 id 為 2, 4 學生的 parent_id = 2 (王曉如)
```
>更新了students表中的parent_id欄位，以建立學生與父母之間的關聯：

<font color=#FF0000> Out [14]: </font>
![UPDATE SET WHERE](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F3-4.png?alt=media&token=664ee05d-ac7c-4167-8708-8f144a790544)

使用 INNER JOIN 合併資料表查詢學生與家長的詳細資料
<font color=#0000FF> In [15]: </font>

```sql
SELECT 
    students.id AS 小孩編號,
    students.name AS 學生姓名, 
    parents.name AS 父母名稱, 
    parents.phone AS 父母電話, 
    parents.gender AS 父母性別
FROM students
INNER JOIN parents on parents.id = students.parent_id;
```
>通過INNER JOIN將students表與parents表聯接，使用students.parent_id和parents.id作為關聯條件。這樣可以列出每個學生及其對應的父母信息。

<font color=#FF0000> Out [15]: </font>
![SELECT AS FROM INNER JOIN ON](https://firebasestorage.googleapis.com/v0/b/pictureforu-3b8e9.appspot.com/o/SQL%E5%B0%8F%E7%AF%80%E4%BD%9C%E6%A5%AD%EF%BC%9A%E4%B8%BB%E9%8D%B5%E3%80%81%E5%A4%96%E4%BE%86%E9%8D%B5%E3%80%81inner%20join%2F3-5.png?alt=media&token=5545ee06-fcaa-4b84-b072-eaf17ecfd287)

## 回顧
在本節，我們練習了：
一、規劃外來鍵與資料表拆分
二、主鍵設定方式以及ID 自動地增方法
三、搭配 Where 條件，合併資料表查詢
四、使用 inner join，合併資料表查詢

如果沒有問題的話，那我們就可以前往下一章節囉。d(d＇∀＇)