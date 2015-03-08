## Operators（操作符）

### ADD 加法操作符（ + ）

如果兩個操作數都是數字，執行常規加法計算。

```javascript
  5 + 5                 // 10 
```

如果其中一個操作數是NaN，返回NaN.

```javascript
  NaN + 5               // NaN
```

如果其中一個操作數是字符串，則應用以下規則：

```javascript
  // 兩個操作數都是字符串，則拼接兩個字符串
  "5" + "5"             // "55"
  
  // 只有一個操作數是字符串，則把另一個操作數轉換為字符串，再拼接
  "5" + 3               // "53"
  
```

如果其中一個操作數是對象、數字或Boolean值，另一個操作數是**字符串**，則先調用它們的toString()方法取得相應字符串值，再拼接.

```javascript
  true + "1"            // "true1"
  false + "2"           // "false2"

```

如果其中一個操作數是undefined或null，另一個操作數是**字符串**，則先調用它們的String()方法取得相應字符串值，再拼接。

```javascript
  null + "1"            // "null1"
  undefined + "2"       // "undefined2"
```

如果其中一個操作數是對象、數字或Boolean值，另一個操作數是**數字**，則先調用它們的Number()方法取得相應字符串值，再拼接.

```javascript
  true + 1              // 2  （ Number(true) => 1 ）
  false + 2             // 2  （ Number(false) => 0 ）
  
  null + 1              // 1  （ Number(null) => 0）
  undefined + 1         // NaN（Number(undefined) => NaN）

```

### Logical NOT 邏輯非（!）

邏輯非操作符首先將它的操作數轉換成為Boolean值，再對其求反。

邏輯非操作符僅返回Boolean值。

```javascript
  !false                // true
  !"blue"               // false ( Boolean("blue") => true )
  !""                   // true  ( Boolean("") => false )
  !1234                 // false ( Boolean(1234) => true )
  !0                    // true  ( Boolean(0) => false )
  !NaN                  // true  ( Boolean(NaN) => false )
  !null                 // true  ( Boolean(null) => false )
  !undefined            // true  ( Boolean(undefined) => false )
```

### Logical AND 邏輯與（&&）

在邏輯與操作中，如果第一個操作數**可以決定結果**，將不會對第二個操作數求值。

```javascript
  true && 123           // true

```

它遵循以下規則：

```javascript
  var obj = { name : 'object' };
  
  // 如果第一個操作數是對象，則返回第二個操作數
  obj && true           // true 
  
  // 如果第二個操作數是對象，僅當第一個操作數為真時，才返回此對象
  true && obj           // { name : 'object' }
  123 && obj            // { name : 'object' }
  
  // 如果其中一個操作數是NaN，null或undefined，另一個操作數為真時，則返回這些值
  true && NaN           // NaN
  123 && null           // null
  "sky" && undefined    // undefined
  
  // 當另一個操作數不為真時，結果如下：
  false && null         // false
  undefined && false    // undefined
```

### Logical OR 邏輯或（ || ）

與邏輯與操作類似，**當第一個操作數為真時**，將不會對第二個操作數求值。

它遵循以下規則：

```javascript
  var obj = { name : 'object' };
  
  // 如果第一個操作數是對象，則返回第一個操作數
  obj || true           // { name : 'object' } 
  
  // 如果第一個個操作數不為真，則返回第二個操作數
  false || obj          // { name : 'object' }
  
  // 當兩個操作數都是NaN、null或undefined時，才返回這些值
  NaN || NaN            // NaN

```

### 相等（=）和 不相等（!=）

這兩個操作符都會先轉換操作數（強制轉型），然後再比較相等性。

```javascript
  // 如果其中一個操作符是Boolean值，則先將它轉換為數值，再進行相等性比較
  false == 1            // false （ Number(false) => 0 ）
  true == 1             // true  （ Number(true) => 0 ）
  
  // 如果一個操作數是數值，另一個是字符串，則先將字符串轉換為數值，再進行比較
  "cat" == 12           // false （ Number("cat") => NaN ）
  "123" == 123          // true  （ Number("123") => 123 ）
  
  // null 和 undefied 是相等的
  null == undefined     // true
  
  // null 和 undefined與其它值進行比較，不會進行強制轉換
  undefined == 0        // false
  nul == 0              // false
  
  // NaN 與任何值都不等
  NaN == NaN            // false
  NaN != NaN            // true

```

### 全等（=）和 不全等（!=）

這兩個操作符，在比較相等性之前，不會強制轉型。

```javascript
  "123" === 123         // false
  
  // null 和 undefined 不全等
  null === undefined    // false
```