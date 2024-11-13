---
title: Lady YinMin's Regards
date: 2024-11-09 19:50:20
tags:
description: Lady YinMin's Regards is a legendary item in CodeWars.
---
The item was named after user Lady YinMin. This coder was known as one of the community lead of HexSchool.
---

----

### [「 Break camelCase - 打斷駝峰命名 」](https://www.codewars.com/kata/5208f99aee097e6552000148)
將駝峰命名法的字符串分隔為單詞並在單詞之間添加空格的函數，我們需要識別每個大寫字母，並在它前面插入一個空格。

```js
function solution(string) {
  // 使用正則表達式來識別大寫字母，並在其前面加上空格
  return string.replace(/([A-Z])/g, ' $1');
}

// 範例使用
console.log(solution("camelCasing")); // 輸出: "camel Casing"
console.log(solution("identifier"));  // 輸出: "identifier"
console.log(solution(""));            // 輸出: ""
```
>**正則表達式：**
>><code>([A-Z])</code>：這個部分用來匹配字符串中的每個大寫字母。[A-Z] 匹配任意大寫字母，括號 () 用於捕獲匹配的字母。
>><code>g</code> 標誌表示全局匹配，這樣可以替換字符串中所有的大寫字母。

>**替換：**
>><code>replace</code> 方法用來替換匹配到的部分。
>><code>' $1'</code>：這個表示將匹配到的大寫字母用空格加上該字母來替換，其中 $1 代表第一個捕獲組（即大寫字母本身）。


----

### [「 Incrementer - 加法器 」](https://www.codewars.com/kata/590e03aef55cab099a0002e8)
要實現 incrementer 函數，我們需要遍歷給定的數字陣列，並將每個數字增加其在陣列中的位置（從1開始計算）。
如果結果是兩位數，只保留結果的最後一位數。

```js
function incrementer(nums) {
  // 如果陣列為空，返回空陣列
  if (nums.length === 0) {
    return [];
  }

  // 使用 map 遍歷陣列，並對每個元素進行計算
  return nums.map((num, index) => {
    // 計算每個數字加上其位置（位置從1開始，因此是 index + 1）
    let incrementedValue = num + index + 1;
    // 只保留最後一位數
    return incrementedValue % 10;
  });
}

// 範例使用
console.log(incrementer([1, 2, 3])); // 輸出: [2, 4, 6]
console.log(incrementer([4, 6, 9, 1, 3])); // 輸出: [5, 8, 2, 5, 8]
console.log(incrementer([])); // 輸出: []

```
>**檢查空陣列：**首先檢查輸入陣列是否為空，如果是，則返回一個空陣列。
>**遍歷和計算：**使用 <code>map</code> 函數遍歷每個數字。
>>index 參數表示當前數字在陣列中的索引位置。
>>對於每個數字，計算 <code>num + index + 1</code>，因為位置是從1開始計算的。
>>使用<code>% 10</code> 操作符來確保只保留結果的最後一位數。
>>返回結果：<code>map</code> 函數會返回一個新的陣列，其中包含每個計算後的數字。

----

### [「Exes and Ohs - X 與 O 」](https://www.codewars.com/kata/55908aad6620c066bc00002a) 
要實現 XO 函數，我們需要檢查字符串中 'x' 和 'o' 字符的數量是否相等。
這個函數“應該”對大小寫不敏感，並且在字符串中不包含 'x' 和 'o' 時應返回 true。

```js
function XO(str) {
    // 將字符串轉換為小寫，確保不區分大小寫
    str = str.toLowerCase();
    
    // 計算 'x' 和 'o' 的數量
    let countX = 0;
    let countO = 0;
    
    for (let char of str) {
        if (char === 'x') {
            countX++; // 如果字符是 'x'，增加 x 的計數
        } else if (char === 'o') {
            countO++; // 如果字符是 'o'，增加 o 的計數
        }
    }
    
    // 返回 'x' 和 'o' 的數量是否相等
    return countX === countO;
}

// 範例使用
console.log(XO("ooxx")); // 輸出: true
console.log(XO("xooxx")); // 輸出: false
console.log(XO("ooxXm")); // 輸出: true
console.log(XO("zpzpzpp")); // 輸出: true
console.log(XO("zzoo")); // 輸出: false
```
>**轉換為小寫：**首先，我們將整個字符串轉換為小寫，這樣就能確保比較時不區分大小寫。
>**計數字符：**
>>初始化 <code>countX</code> 和 <code>countO</code> 為 0，用來計算 'x' 和 'o' 的數量。
>>使用 <code>for...of</code>迴圈遍歷字符串中的每個字符。
>>如果字符是 'x'，則增加 <code>countX</code>
>>如果字符是 'o'，則增加 <code>countO</code>。
----

### [「 Likes Vs Dislikes - 喜歡與不喜歡 」](https://www.codewars.com/kata/62ad72443809a4006998218a)
要實現<code>likeOrDislike</code> 函數，我們需要模擬 YouTube 的按鈕行為規則。具體來說，我們需要處理一個按鈕輸入列表，並根據以下規則返回最終狀態：
-初始狀態是 Nothing。
-如果按下的按鈕與當前狀態相同，則狀態變為 Nothing（即取消當前狀態）。
-如果按下的按鈕與當前狀態不同，則狀態變為該按鈕的狀態（Like 或 Dislike）。
-如果輸入列表為空，返回 Nothing。

```js
function likeOrDislike(buttons) {
  let currentState = "Nothing"; // 初始狀態設置為 Nothing

  for (let button of buttons) {
    if (button === currentState) {
      currentState = "Nothing"; // 如果按鈕與當前狀態相同，取消狀態
    } else {
      currentState = button; // 否則，更新狀態為按鈕的狀態
    }
  }

  return currentState; // 返回最終狀態
}

// 範例使用
console.log(likeOrDislike(["Dislike"])); // 輸出: "Dislike"
console.log(likeOrDislike(["Like", "Like"])); // 輸出: "Nothing"
console.log(likeOrDislike(["Dislike", "Like"])); // 輸出: "Like"
console.log(likeOrDislike(["Like", "Dislike", "Dislike"])); // 輸出: "Nothing"
console.log(likeOrDislike([])); // 輸出: "Nothing"
```
>**初始狀態：**我們從 Nothing 開始，表示當前沒有任何按鈕被激活。
>>如果相同，則將狀態設置為 Nothing，表示取消當前狀態。
>>如果不同，則更新狀態為該按鈕的狀態。

>**返回結果：**最後返回 currentState，這是根據按鈕輸入列表計算出的最終狀態。

----

### [「 Count of positives / sum of negatives - 算正整數與負總數合 」](https://www.codewars.com/kata/576bb71bbbcf0951d5000044)
實現 countPositivesSumNegatives 函數，我們需要遍歷給定的整數數組，計算正數的個數以及負數的總和。當輸入數組為空或為 null 時，應返回一個空數組。

```js
function countPositivesSumNegatives(input) {
  if (!input || input.length === 0) {
    return []; // 如果輸入為空或為 null，返回空數組
  }

  let countPositives = 0; // 用來計算正數的個數
  let sumNegatives = 0;   // 用來計算負數的總和

  for (let number of input) {
    if (number > 0) {
      countPositives++; // 如果是正數，增加計數
    } else if (number < 0) {
      sumNegatives += number; // 如果是負數，累加到總和中
    }
  }

  return [countPositives, sumNegatives]; // 返回包含正數個數和負數總和的數組
}

// 範例使用
console.log(countPositivesSumNegatives([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, -11, -12, -13, -14, -15])); // 輸出: [10, -65]
console.log(countPositivesSumNegatives([])); // 輸出: []
console.log(countPositivesSumNegatives(null)); // 輸出: []
```
>**檢查輸入：**首先檢查輸入是否為空或為 <code>null</code>如果是，直接返回空數組 []。
>**初始化計數和總和：**
>><code>countPositives</code>用來計算正數的個數，初始值為 0。
>><code>sumNegatives</code>用來計算負數的總和，初始值為 0。

>**遍歷數組：**使用<code>for...of</code>迴圈遍歷數組中的每個元素。
>>如果元素是正數，將<code>countPositives</code>增加 1。
>>如果元素是負數，將該元素加到<code>sumNegatives</code>中。

>返回結果：最後返回一個數組，第一個元素是正數的個數，第二個元素是負數的總和。

----

### [「 Count characters in your string - 記數字串中的字元 」](https://www.codewars.com/kata/52efefcbcdf57161d4000091)
實現一個函數 count，用來計算字符串中每個字符出現的次數，我們可以使用一個對象來存儲每個字符及其對應的出現次數。當字符串為空時，我們應返回一個空的對象 {}。

```js
function count(string) {
  const charCount = {}; // 用來存儲字符計數的對象

  for (let char of string) { // 遍歷字符串中的每一個字符
    if (charCount[char]) {
      charCount[char]++; // 如果字符已存在於對象中，增加計數
    } else {
      charCount[char] = 1; // 如果字符不存在，初始化計數為 1
    }
  }

  return charCount; // 返回字符計數對象
}

// 範例使用
console.log(count("aba")); // 輸出: { a: 2, b: 1 }
console.log(count(""));    // 輸出: {}
```
>**初始化對象：**創建一個空對象 <code>charCount </code>來存儲每個字符的計數。
>**遍歷字符串：**使用 <code> for...of </code>迴圈遍歷字符串中的每一個字符。


### [「 V A P O R C O D E 」](https://www.codewars.com/kata/5966eeb31b229e44eb00007a)
實現 vaporcode 函數，將一個句子轉換為 V A P O R W A V E 風格，我們需要將所有字母轉換為大寫並在每個字母或特殊字符之間加入兩個空格，同時忽略原始句子中的空格。

```js
function vaporcode(string) {
  return string
    .replace(/\s+/g, '') // 移除所有空格
    .toUpperCase()       // 將所有字母轉為大寫
    .split('')           // 將字符串分割成單個字符的數組
    .join('  ');         // 在每個字符之間加入兩個空格
}

// 範例使用
console.log(vaporcode("Lets go to the movies"));      // 輸出: "L  E  T  S  G  O  T  O  T  H  E  M  O  V  I  E  S"
console.log(vaporcode("Why isn't my code working?")); // 輸出: "W  H  Y  I  S  N  '  T  M  Y  C  O  D  E  W  O  R  K  I  N  G  ?"
```
>**移除空格：**使用<code> replace(/\s+/g, '')</code>來移除所有空格，確保只有字母和其他字符被處理。
>**轉換為大寫：**使用<code> toUpperCase()</code>將字符串中的所有字母轉換為大寫，符合 V A P O R W A V E 的風格。
>**分割和重組：**使用<code> split('')</code>將字符串分割成單個字符的數組，然後使用<code> join('  ') </code>在每個字符之間插入兩個空格來重組字符串。

----

### [「 Love vs friendship - 愛與友情 」](https://www.codewars.com/kata/59706036f6e5d1e22d000016)
要計算一個單詞中每個字母的位置值之和，我們可以利用字母在字母表中的位置來進行計算。
字母 'a' 對應位置 1，'b' 對應位置 2，以此類推，直到 'z' 對應位置 26。這可以通過計算字母的 ASCII 值來實現。
在 JavaScript 中，我們可以使用<code>charCodeAt</code>方法來獲取字母的 ASCII 值，然後減去 96 *（因為 'a' 的 ASCII 值是 97）* 來得到字母的位置值。

```js
function wordsToMarks(string) {
  return string.split('').reduce((sum, char) => sum + (char.charCodeAt(0) - 96), 0);
}

// 範例使用
console.log(wordsToMarks("love"));      // 輸出: 54
console.log(wordsToMarks("friendship")); // 輸出: 108
```
>**split('') 方法：**將字符串分割成單個字符的數組
>**reduce 方法：**遍歷字符數組，計算每個字符的字母位置值之和。<code>char.charCodeAt(0)</code>- 96 用來計算字符的字母位置值。
>**累加和：**<code>reduce</code> 的初始值設為 0，然後逐步累加每個字母的數值。

----

### [「 List Filtering - 清單過濾 」](https://www.codewars.com/kata/53dbd5315a3c69eed20002dd)
<code>filter</code>方法允許我們根據指定的條件過濾數組中的元素。在這個情況下，我們需要檢查每個元素是否為數字類型。

```js
function filter_list(l) {
  return l.filter(item => typeof item === 'number');
}

// 範例使用
console.log(filter_list([1, 2, 'a', 'b'])); // 輸出: [1, 2]
console.log(filter_list([1, 'a', 'b', 0, 15])); // 輸出: [1, 0, 15]
console.log(filter_list([1, 2, 'aasf', '1', '123', 123])); // 輸出: [1, 2, 123]
```
>**使用 filter 方法：** <code>filter</code>方法會遍歷數組中的每一個元素，並根據提供的函數返回一個新數組，該函數返回 true 的元素會被保留。
>**檢查類型：**<code>typeof item === 'number'</code>用於檢查元素是否為數字類型。只有當元素是數字時，這個條件才會返回 true，從而保留該元素。

### [「 Count Odd Numbers below n - 找尋 n 以下的偶數數量 」](https://www.codewars.com/kata/59342039eb450e39970000a6)
奇數是從 1 開始以 2 為間隔增加的數字序列。
因此，對於一個數字 n，小於 n 的奇數的數量可以通過整數除法來計算，即 n/2（在 JavaScript 中使用 <code>Math.floor(n/2)</code>）。

```js
function oddCount(n) {
  return Math.floor(n / 2);
}

// 範例使用
console.log(oddCount(7));  // 輸出: 3
console.log(oddCount(15)); // 輸出: 7
```
>**整數除法：**<code>Math.floor(n/2)</code>計算小於 n 的正奇數的數量。這是因為每兩個連續的整數中有一個是奇數。

-----

### [「 Find the odd int - 找尋奇數整數 」](https://www.codewars.com/kata/54da5a58ea159efa38000836)
利用按位異或運算符（XOR）。
因為 XOR 的特性：任何數字與自身 XOR 將得到 0，且任何數字與 0 XOR 將得到自身。這意味著，如果我們對數組中的所有數字進行 XOR 運算，成對出現的數字會互相抵消，剩下的就是出現奇數次的數字。

```js
function findOdd(A) {
  return A.reduce((acc, num) => acc ^ num, 0);
}

// 範例使用
console.log(findOdd([7])); // 輸出: 7
console.log(findOdd([0])); // 輸出: 0
console.log(findOdd([1, 1, 2])); // 輸出: 2
console.log(findOdd([0, 1, 0, 1, 0])); // 輸出: 0
console.log(findOdd([1, 2, 2, 3, 3, 3, 4, 3, 3, 3, 2, 2, 1])); // 輸出: 4
```
>**使用 reduce 方法：** <code>reduce</code>方法會遍歷數組中的每一個元素，並將其與累加器進行 XOR 運算。初始值設為 0。
>**XOR 運算：**<code>acc ^ num</code>表示累加器與當前數字進行 XOR 運算。由於成對出現的數字會互相抵消，最終累加器中只會剩下出現奇數次的數字。

----

### [「 Filter the number - 過濾出數字 」](https://www.codewars.com/kata/55b051fac50a3292a9000025)
要從混合了數字和字母的字符串中提取出所有數字，我們可以使用 JavaScript 中的“正則表達式”來過濾出數字。

```js
function filterString(value) {
  // 使用正則表達式匹配數字，並將其連接成一個字符串
  return parseInt(value.replace(/\D/g, ''), 10);
}

// 範例使用
const input = "a1b2c3";
const output = filterString(input);
console.log(output);  // 輸出: 123
```
>**使用正則表達式：** **<code>\D</code>** 是一個正則表達式，用來匹配非數字字符。g 是全域標誌，表示匹配所有非數字字符。
>**replace:** **<code>replace(/\D/g, '')</code>** 將所有非數字字符替換為空字符串，這樣只剩下數字。
>**轉換為數字：**使用 <code>parseInt</code> 將結果字符串轉換為整數。這樣可以確保返回的結果是數字類型，而不是字符串。

----

### [「 Testing 1-2-3 - 測試 1-2-3 」](https://www.codewars.com/kata/54bf85e3d5b56c7a05000cf9)
要在每行文本前面加上行號，我們可以使用 JavaScript 中的 map 方法來遍歷每個字符串，然後將行號與字符串組合起來。
行號從 1 開始，格式為 n: string，其中 n 是行號。

```js
var number = function(array) {
  return array.map((line, index) => {
    return `${index + 1}: ${line}`;
  });
};

// 範例使用
const input = ["a", "b", "c"];
const output = number(input);
console.log(output);  // 輸出: ["1: a", "2: b", "3: c"]
```
>**使用 map 方法：**<code>map</code> 方法會遍歷數組中的每一個元素，並返回一個新數組，其中每個元素都是根據提供的函數轉換而來的。
>**計算行號：**在<code>map</code>方法中，我們使用箭頭函數來處理每個字符串。index 是當前元素的索引，我們在計算行號時加 1，因為行號是從 1 開始的。
>**格式化輸出：**使用模板字符串（template literals）將行號和字符串組合成所需的格式，即 <code>n: string</code>

----

### [「 Categorize New Member - 分類新成員 」](https://www.codewars.com/kata/5502c9e7b3216ec63c0001aa)
要為槌球俱樂部的會員分類，我們需要根據輸入的年齡和障礙分來判斷每個潛在會員應被歸類為 "Senior" 還是 "Open"。
根據給定的條件：
**‧** 如果年齡至少為 55 歲，且障礙分大於 7，則該會員屬於 "Senior" 類別。
**‧** 否則，該會員屬於 "Open" 類別。

```js
function openOrSenior(data) {
  return data.map(([age, handicap]) => {
    if (age >= 55 && handicap > 7) {
      return "Senior";
    } else {
      return "Open";
    }
  });
}

// 範例使用
const input = [[18, 20], [45, 2], [61, 12], [37, 6], [21, 21], [78, 9]];
const output = openOrSenior(input);
console.log(output);  // 輸出: ["Open", "Open", "Senior", "Open", "Open", "Senior"]
```
>**遍歷資料：**使用<code>map</code>方法遍歷每一對年齡和障礙分的數據。
>**判斷條件：**對於每個成員，檢查他的年齡是否大於等於 55 且障礙分是否大於 7。如果兩者都滿足，則將該成員分類為 "Senior"；否則，分類為 "Open"。
>**返回結果：**<code>map</code> 方法會返回一個新陣列，其中包含每個成員的分類結果。

----

### [「 Total amount of points 總分數 」](https://www.codewars.com/kata/5bb904724c47249b10000131)
要計算足球隊在錦標賽中獲得的總分數，需要"遍歷"每場比賽的結果，然後根據比賽結果計算分數。
每場比賽的結果以 "x:y" 的格式呈現，其中 x 是我們隊的得分，y 是對手的得分。
根據給定的規則：
**‧** 如果 x > y，我們獲得 3 分（勝利）。
**‧** 如果 x < y，我們獲得 0 分（失敗）。
**‧** x = y，我們獲得 1 分（平局）。

```js
function points(games) {
    let totalPoints = 0;

    for (let game of games) {
        const [x, y] = game.split(':').map(Number);

        if (x > y) {
            totalPoints += 3; // 勝利
        } else if (x === y) {
            totalPoints += 1; // 平局
        }
        // 如果 x < y，則 totalPoints 不變，因為我們獲得 0 分
    }

    return totalPoints;
}

// 範例使用
console.log(points(["3:1", "2:2", "0:1", "4:0", "2:3", "1:1", "2:0", "1:3", "0:0", "3:2"]));  // 輸出: 17
```
>**初始化總分數：**用變數<code>totalPoints</code>來累計我們隊的總分數，初始值為 0。
>**遍歷比賽結果：**使用<code>for...of</code>迴圈遍歷 games 陣列中的每個比賽結果。
>**分割和轉換得分：**對於每個比賽結果，使用<code>split(':')</code>將字符串分割為兩個部分，然後用<code>map(Number)</code>將它們轉換為數字。

>**計算分數：**
>>如果 x > y，我們增加 3 分。
>>如果 x === y，我們增加 1 分。
>>如果 x < y，我們不增加分數。

>**返回總分數：**最後，返回計算出的<code>totalPoints</code>。

----

### [「 Get the Middle Characte - 獲取中間字元 」](https://www.codewars.com/kata/56747fd5cb988479af000028)
從一個非空字符串中返回中間的字符，我們需要根據字符串的長度來決定是返回一個字符還是兩個字符。
**‧** 如果字符串的長度是奇數，則返回中間的單個字符。
**‧** 如果字符串的長度是偶數，則返回中間的兩個字符。

```js
function getMiddle(s) {
    const length = s.length;
    const middleIndex = Math.floor(length / 2);

    // 如果字符串長度是偶數，返回中間兩個字符
    if (length % 2 === 0) {
        return s[middleIndex - 1] + s[middleIndex];
    } else {
        // 如果字符串長度是奇數，返回中間的單個字符
        return s[middleIndex];
    }
}

// 範例使用
console.log(getMiddle("test"));    // 輸出: "es"
console.log(getMiddle("testing")); // 輸出: "t"
console.log(getMiddle("middle"));  // 輸出: "dd"
console.log(getMiddle("A"));       // 輸出: "A"
```
>**計算字符串長度：**首先獲取字符串的長度 length，然後計算中間索引 middleIndex，使用 Math.floor(length / 2) 來確定中間位置。
>**判斷長度奇偶：**
>>*偶數長度：*如果<code>length % 2 === 0</code>，表示字符串長度是偶數，則返回從<code>middleIndex - 1</code>開始的兩個字符
>>*奇數長度：*如果字符串長度是奇數，則直接返回<code>middleIndex</code>位置的字符。
----

### [「 Rock Paper Scissors! - 剪刀石頭布！ 」](https://www.codewars.com/kata/5672a98bdbdd995fad00000f)
要實現「石頭、剪刀、布」遊戲的勝負判斷，需要比較兩個玩家的選擇，然後根據遊戲規則決定誰贏了，或者是否平局。
遊戲規則如下：
**‧** 剪刀贏紙
**‧** 石頭贏剪刀
**‧** 布贏石頭
**‧** 如果兩個玩家選擇相同，則為平局
使用條件判斷來實現這個邏輯。

```js
const rps = (p1, p2) => {
    if (p1 === p2) {
        return "Draw!";
    }

    if (
        (p1 === "scissors" && p2 === "paper") ||
        (p1 === "rock" && p2 === "scissors") ||
        (p1 === "paper" && p2 === "rock")
    ) {
        return "Player 1 won!";
    } else {
        return "Player 2 won!";
    }
};

// 範例使用
console.log(rps("scissors", "paper"));  // 輸出: "Player 1 won!"
console.log(rps("scissors", "rock"));   // 輸出: "Player 2 won!"
console.log(rps("paper", "paper"));     // 輸出: "Draw!"
```

>**平局判斷：**首先檢查 p1 和 p2 是否相等。如果相等，則返回 "Draw!"，表示平局。

>**勝負判斷：**
>>使用條件判斷來檢查玩家1是否獲勝的情況：
>>>剪刀對紙
>>>石頭對剪刀
>>>布對石頭

>>如果上述條件不成立，則玩家2獲勝。

----

### [「 I love you, a little , a lot, passionately ... not at all - 愛你、還好、最愛……不愛你 」](https://www.codewars.com/kata/57f24e6a18e9fad8eb000296)
Q:需要確定當撕掉最後一片花瓣時，應該說哪一句話。
A:由於這些短語是循環的，我們可以使用模運算（取餘數）來確定應該說哪一句話。
這些短語按順序排列如下：
「
"I love you"
"a little"
"a lot"
"passionately"
"madly"
"not at all"
」
如果有超過 6 片花瓣，我們就從頭開始重複這些短語。
因此，對於給定的花瓣數量 nbPetals，我們可以使用 (nbPetals - 1) % 6 來找到對應的短語索引。
這裡的 - 1 是因為索引從 0 開始。

```JS
function howMuchILoveYou(nbPetals) {
    const phrases = [
        "I love you",
        "a little",
        "a lot",
        "passionately",
        "madly",
        "not at all"
    ];
    
    // 計算對應的短語索引
    const index = (nbPetals - 1) % phrases.length;
    
    // 返回對應的短語
    return phrases[index];
}

// 範例使用
console.log(howMuchILoveYou(7));  // 輸出: "I love you"
console.log(howMuchILoveYou(3));  // 輸出: "a lot"
console.log(howMuchILoveYou(6));  // 輸出: "not at all"
```
>**短語陣列：**用一個陣列 <code>phrases</code> 來存放所有的短語。
>**計算索引：**使用 <code>(nbPetals - 1) % phrases.length</code>來計算對應的短語索引。這樣可以確保即使 nbPetals 超過 6，也能正確循環回到起始短語。
>**返回結果：**根據計算出的索引，返回相應的短語。

----

### [「 Will you make it? - 辦得到嗎？ 」](https://www.codewars.com/kata/5861d28f124b35723e00005e)
Q:計算汽車剩餘的燃油是否足夠支持行駛到加油站的距離。
A:通過比較汽車在剩餘燃油下能行駛的總里程與到加油站的距離來實現。

```JS
const zeroFuel = (distanceToPump, mpg, fuelLeft) => {
  // 計算剩餘燃油能行駛的最大距離
  const maxDistance = mpg * fuelLeft;
  
  // 如果最大距離大於或等於到加油站的距離，則返回 true，否則返回 false
  return maxDistance >= distanceToPump;
};

// 範例使用
console.log(zeroFuel(50, 25, 2)); // 輸出: true
console.log(zeroFuel(100, 25, 3)); // 輸出: false
```
>**計算最大可行駛距離：**使用 *mpg * fuelLeft*計算在剩餘燃油下汽車能行駛的最大距離。
>>mpg 是每加侖可以行駛的英里數。 *(milePerGallons)*
>>fuelLeft 是剩餘的加侖數。

>**比較距離：**將計算出的最大可行駛距離與到加油站的距離 distanceToPump 進行比較。
>>如果最大可行駛距離大於或等於 distanceToPump，則說明汽車可以到達加油站，返回 true。
>>否則，返回 false

----

### [「 Training JS #8: Conditional statement--switch - Switch 語法 」](https://www.codewars.com/kata/572059afc2f4612825000d8a)
使用 switch 語句來完成 howManydays 函數，這個函數接受一個參數 month，並根據月份返回相應的天數。

```js
function howManydays(month) {
  var days;
  switch (month) {
    case 1:
    case 3:
    case 5:
    case 7:
    case 8:
    case 10:
    case 12:
      days = 31;
      break;
    case 4:
    case 6:
    case 9:
    case 11:
      days = 30;
      break;
    case 2:
      days = 28;
      break;
    default:
      // 預設情況下，我們不需要做任何事情，因為所有的月份都已經涵蓋
      break;
  }
  return days;
}

// 範例使用
console.log(howManydays(1));  // 輸出: 31
console.log(howManydays(2));  // 輸出: 28
console.log(howManydays(4));  // 輸出: 30
```
>**switch 語句：**我們使用<code>switch</code>來根據 month 的值選擇執行的代碼塊。
>**case 語句：**每個 case 語句後面跟著一個數值，表示當 month 的值等於該數值時，執行相應的代碼塊。
>>月份 1, 3, 5, 7, 8, 10, 12 都有 31 天。
>>月份 4, 6, 9, 11 有 30 天。
>>月份 2 有 28 天（不考慮閏年）。

>break 語句：每個 case 語句結束後使用 break 語句來防止程式繼續執行後續的 case 語句。

---

### [「 Jaden Casing Strings - 首字大寫 」](https://www.codewars.com/kata/5390bac347d09b7da40006f6)
擴展 JavaScript 的 String 原型，為它添加一個方法 toJadenCase，用來將字串中的每個單詞的首字母大寫。

```js
String.prototype.toJadenCase = function () {
    // 使用 split 方法將字串分割為單詞陣列
    return this.split(' ')
        // 使用 map 方法遍歷每個單詞，將首字母轉為大寫
        .map(word => word.charAt(0).toUpperCase() + word.slice(1))
        // 使用 join 方法將單詞陣列重新組合成字串
        .join(' ');
};

// 範例使用
const quote = "How can mirrors be real if our eyes aren't real";
console.log(quote.toJadenCase()); // 輸出: "How Can Mirrors Be Real If Our Eyes Aren't Real"
```
>**split(' ')方法：**將字串按照空格分割成一個單詞陣列。
>**map() 方法：**遍歷每個單詞，將單詞的首字母轉換為大寫，並保持其餘部分不變。
>>word.charAt(0).toUpperCase() 取得單詞的首字母並轉為大寫。
>>word.slice(1) 取得單詞的其餘部分。
>**join(' ') 方法：**將處理過的單詞陣列重新組合成字串，單詞之間用空格分隔。

----

### [「 Stringy Strings - 細弦字串 」](https://www.codewars.com/kata/563b74ddd19a3ad462000054)
編寫一個函數 stringy，用於生成一個由 1 和 0 交替組成的字串，並且字串以 1 開頭。這個函數會根據給定的 size 來決定字串的長度。

```js
function stringy(size) {
    let result = '';
    for (let i = 0; i < size; i++) {
        // 如果索引是偶數，添加 '1'，否則添加 '0'
        result += i % 2 === 0 ? '1' : '0';
    }
    return result;
}

// 範例使用
console.log(stringy(6));  // 輸出: '101010'
console.log(stringy(4));  // 輸出: '1010'
console.log(stringy(12)); // 輸出: '101010101010'
```
>**初始化字串 result：**我們從一個空字串開始，然後逐步構建目標字串。
>**迴圈 for：**
>>使用一個 <code>for</code> 迴圈從 “0”遍歷到 “size - 1”。
>>在每次迭代中，檢查當前的索引 i 是偶數還是奇數。
>>如果 i 是偶數，則在 <code>result</code>中添加字符 '1'。
>>如果 i 是奇數，則在 <code>result</code>中添加字符 '0'。

----

### [「 Is the string uppercase? - 字串是大寫的嗎？ 」](https://www.codewars.com/kata/56cd44e1aa4ac7879200010b)
擴展 JavaScript 的 String 原型，為它添加一個方法 isUpperCase，用來檢查字串是否完全由大寫字母組成。

```js
String.prototype.isUpperCase = function() {
    // 使用正則表達式檢查字串中是否有小寫字母
    return !/[a-z]/.test(this);
};

// 範例使用
console.log("c".isUpperCase()); // 輸出: false
console.log("C".isUpperCase()); // 輸出: true
console.log("hello I AM DONALD".isUpperCase()); // 輸出: false
console.log("HELLO I AM DONALD".isUpperCase()); // 輸出: true
console.log("ACSKLDFJSgSKLDFJSKLDFJ".isUpperCase()); // 輸出: false
console.log("ACSKLDFJSGSKLDFJSKLDFJ".isUpperCase()); // 輸出: true
```

>**正則表達式<code>/[a-z]/</code>**
>>這個正則表達式用於檢查字串中是否包含任何小寫字母。
>><code>test()</code>方法返回一個布林值，表示字串中是否存在匹配的模式。

>**邏輯運算符 !：** 我們使用<code>!</code>來反轉 <code>test()</code> 方法的結果，因為我們想要檢查字串中是否不包含小寫字母。如果沒有小寫字母，則表示字串是全大寫的，返回 true。

----

### [「 String cleaning - 清掃字串 」](https://www.codewars.com/kata/57e1e61ba396b3727c000251)
編寫一個函數 stringClean，用於移除字串中的所有數字字符，同時保留空格和其他特殊字符。

```js
function stringClean(s) {
    // 使用 replace 方法和正則表達式來移除所有數字
    return s.replace(/[0-9]/g, '');
}

// 範例使用
console.log(stringClean('! !')); // 輸出: '! !'
console.log(stringClean('123456789')); // 輸出: ''
console.log(stringClean('This looks5 grea8t!')); // 輸出: 'This looks great!'
```
>**replace 方法：**這個方法用於替換字串中的某些部分。這裡我們使用正則表達式來匹配所有數字字符。
> **g** 標誌表示全域搜索，確保替換字串中的所有數字字符，而不僅僅是第一個匹配項。

----

### [「 Reversed Strings - 反轉字串 」](https://www.codewars.com/kata/5168bb5dfe9a00b126000018)
使用 JavaScript 的內建方法來實現這個函數 solution，用於反轉給定的字串。

```js
function solution(str) {
    // 將字串轉換為陣列，反轉陣列，然後再轉換回字串
    return str.split('').reverse().join('');
}

// 範例使用
console.log(solution('world')); // 輸出: 'dlrow'
console.log(solution('word'));  // 輸出: 'drow'
```

>**split('') 方法：**將字串分割成一個字符陣列。這裡的空字串 '' 作為分隔符，表示每個字符都會成為陣列中的一個元素。
>**reverse() 方法：**反轉陣列中元素的順序。
>**join('') 方法：**將反轉後的字符陣列重新組合成一個字串。這裡的空字串 '' 作為連接符，表示直接將字符連接在一起，不插入任何額外的字符。

----

### [「 The Feast of Many Beasts - 野獸的盛宴 」](https://www.codewars.com/kata/5aa736a455f906981800360d)
編寫函數 feast，用於檢查動物名稱和菜餚名稱是否符合規則：菜餚名稱的首尾字母必須與動物名稱的首尾字母相同。

```js
function feast(beast, dish) {
    // 檢查動物名稱和菜餚名稱的首尾字母是否相同
    return beast[0] === dish[0] && beast[beast.length - 1] === dish[dish.length - 1];
}

// 範例使用
console.log(feast("great blue heron", "garlic naan")); // 輸出: true
console.log(feast("chickadee", "chocolate cake")); // 輸出: true
console.log(feast("brown bear", "bear claw")); // 輸出: false
```

>**首尾字母檢查：**
>> <code>beast[0] </code>：取得動物名稱的第一個字母。
>> <code>dish[0]</code>：取得菜餚名稱的第一個字母。
>> <code>beast[beast.length - 1]</code>：取得動物名稱的最後一個字母。
>> <code>dish[dish.length - 1]</code>：取得菜餚名稱的最後一個字母。

>**條件判斷：** 使用 <code>&&</code> 來同時檢查首字母和尾字母是否相同，只有兩者都相同時，函數才返回 true。

----

### [「 Remove String Spaces - 移除字串中的空格 」](https://www.codewars.com/kata/57eae20f5500ad98e50002c5)
使用 JavaScript 中的字串方法來實現這個函數 noSpace，用於移除字串中的所有空格。

```js
function noSpace(x) {
    // 使用 replace 方法和正則表達式來移除所有空格
    return x.replace(/\s+/g, '');
}

// 範例使用
console.log(noSpace("8 j 8   mBliB8g  imjB8B8  jl  B")); // 輸出: "8j8mBliB8gimjB8B8jlB"
console.log(noSpace("8 8 Bi fk8h B 8 BB8B B B  B888 c hl8 BhB fd")); // 輸出: "88Bifk8hB8BB8BBBB888chl8BhBfd"
console.log(noSpace("8aaaaa dddd r     ")); // 輸出: "8aaaaaddddr"
```

>**<code>replace</code>：**這個方法用於替換字串中的某些部分。這裡我們使用正則表達式來匹配所有空白字符。
>**正則表達式 <code>/\s+/g：</code>**
>> **<code>\s</code>** 表示匹配任何空白字符（包括空格、制表符等）
>>**<code>+</code>** 表示匹配一次或多次前面的模式，即一個或多個空白字符。
>>**<code>g</code>** 標誌表示全域搜索，確保替換字串中的所有空白字符，而不僅僅是第一個匹配項。

----

### [「 Thinkful - Logic Drills: Traffic light - 紅綠燈 」](https://www.codewars.com/kata/58649884a1659ed6cb000072/)
完成函數 updateLight , 根據當前的燈光狀態返回下一個狀態。

```JS
function updateLight(current) {
    // 根據當前狀態返回下一個狀態
    if (current === "green") {
        return "yellow"; // 綠燈變黃燈
    } else if (current === "yellow") {
        return "red"; // 黃燈變紅燈
    } else if (current === "red") {
        return "green"; // 紅燈變綠燈
    } else {
        throw new Error("Invalid light state"); // 處理無效的輸入
    }
}
```

>**條件判斷：**使用 <code>if-else</code> 結構來檢查當前的燈光狀態，並返回相應的下一個狀態。
>**錯誤處理：**如果輸入的燈光狀態無效，則拋出一個錯誤，這樣可以幫助我們檢查不正確的使用情況。

------

### [「 Basic Mathematical Operations - 基礎運算符號 」](https://www.codewars.com/kata/57356c55867b9b7a60000bd7)
通過條件判斷來實現函數 basicOp，以執行基本的數學運算（加、減、乘、除）。
函數將根據提供的運算符對兩個數字進行計算並返回結果。

```JS
function basicOp(operation, value1, value2) {
    // 根據運算符進行對應的計算
    switch (operation) {
        case '+':
            return value1 + value2; // 加法
        case '-':
            return value1 - value2; // 減法
        case '*':
            return value1 * value2; // 乘法
        case '/':
            return value1 / value2; // 除法
        default:
            throw new Error("Invalid operation"); // 處理無效的運算符
    }
}
```

>**<code>switch</code> 語句：**使用 <code>switch</code> 語句來根據 <code>operation</code>的值選擇執行哪一種運算。
>**加法、減法、乘法、除法：** 對應不同的運算符（+, -, *, /）執行相應的數學運算。
>**錯誤處理：**如果提供的運算符無效，則拋出一個錯誤，這樣可以幫助我們檢查不正確的使用情況。

------

### [「 Even or Odd - 偶數或奇數 」](https://www.codewars.com/kata/53da3dbb4a5168369a0000fe)
函數 evenOrOdd。檢查傳入的整數是偶數還是奇數，然後返回相應的字串 "Even" 或 "Odd"。

```JS
function evenOrOdd(number) {
    // 使用模運算符 % 來判斷數字是偶數還是奇數
    if (number % 2 === 0) {
        return "Even"; // 如果數字除以 2 的餘數為 0，則是偶數
    } else {
        return "Odd";  // 否則是奇數
    }
}
```

>**模運算符 %：** 用來計算除法的餘數。當 number % 2 等於 0 時，表示該數字是偶數。
>**條件判斷：** 使用 <code>if</code>語句來檢查 number % 2 === 0，如果為真，則返回 "Even"；否則返回 "Odd"