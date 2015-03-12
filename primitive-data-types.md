## 基本數據類型（Primitive Types）

### Undefined
Undefined類型只有一個特殊值: *undefined*。當使用*var*定義變量后沒有對其初始化，這個變量的值為*undefined*。

```javascript
  var type;
  alert(type);    // undefined
```

當一個變量完全沒有被定義，對其使用alert()方法將會報錯。

```javascript
  var type;
  alert(data);    // error。因為data完全沒有定義過。
```

可以使用typeof方法進行驗證。不過typeof方法對於未初始化和未定義的變量，都返回*undefined*，會比較confuse。

```javascript
  var type;
  typeof(type);    // undefined
  typeof(data);    // undefined
```

------

### Null

Null類型同樣只有一個特殊值：*null*。

邏輯上null的值指向一個空對象（empty object pointer），因此使用typeof方法檢測null值時，返回"object"（這個bug有望在ECMAScript 6中修復）。

```javascript
  var type = null;
  typeof(null);    // "object"
```

留意下文，是‘intentional absence’。所以若定義變量時，意在保存object，可以先將其初始化為null。
> null value: primitive value that represents the intentional absence of any object value ([ECMA-262, 5.1 Edition, 4.3.11](http://www.ecma-international.org/ecma-262/5.1/#sec-4.3.11)).

null並不是object，它只是基礎數據類型的一種，你不能給它定義新屬性

```javascript
  var obj = {};
  null === obj;    // false
```

既然null不是object，為何typeof方法返回"object"？因為這是規定([The typeof Operator](http://www.ecma-international.org/ecma-262/5.1/#sec-11.4.3))

------
### undefined 與 null

 * *undefined*意為“未賦值”，而*null*意為“已賦值為nothing”。

 * *undefined*的東西不存在，*null*存在，但真正的值未知。

 * 這有點像現在與未來。*undefined*是當下，因為我們已經知道它不存在；而*null*則是未來，我們都知道未來存在，只是不知道它的樣子而已。

------

### Boolean

Boolean類型有true和false兩個字面值。

此兩值區分大小寫：True 和 False（及其它混合大小寫的形式），都不是Boolean值。

此兩值跟數字值不是一回事：true 不等於 1， false不等於0。

ECMAScript中所有類型的值，都有與這兩個Boolean值等價的值（ 調用 Boolean() 方法進行轉換 ）。


| 數據類型  | 轉換為true的值  | 轉換為false的值  |
| :------: | :-----------: | :------------: |
| Boolean  |  true         | false          |
| String   |  非空字符串     | "" （空字符串）  |
| Number   |  非0數字       | 0 和 NaN        |
| Object   |  任何object    | null           |
| Undefined|  n/a          | undefined      |

**注意：** if 語句自動執行Boolean轉換。

------

### Number

**[ 基本概念 ]**

- 使用IEEE754格式來表示**整數**和**浮點數**

- e表示法。例如：3.125e7表示3.125 * 10^(7)

- 0.1 + 0.2 = 0.30000000000000004（基於IEEE754格式的捨入誤差）

- 數值範圍 5e-324(`Number.MIN_VALUE`) 到 1.7976931348623157e+308(`Number.MAX_VALUE`)。

- 小於`Number.MIN_VALUE`的值會顯示-Infinity，大於`Number.MAX_VALUE`的值會顯示Infinity，這兩種值都無法參加下一次的運算。


**[ NaN ]**

NaN是一個特殊的**數值(Number)**。用來表示意在返回數值的操作失敗了（uses to indicate when an operation intended to return a number has failed），以避免報錯。

例如，在其他編程語言中，任意數值除以0將會報錯，代碼停止運行。但在ECMAScript中，任何數值除以0會返回NaN，不會影響其它代碼執行。

- 任何涉及NaN的操作，都會返回NaN
- NaN與任何值都不相等，包括其本身

  ```javascript
    Boolean(NaN === NaN)  // false
    Boolean(NaN == NaN)   // false
  ```
- isNaN() 方法

  ```javascript
    isNaN(NaN)          // true
    isNaN(10)           // false（是數字）
    isNaN("10")         // false（可以轉換為數字10）
    isNaN("blue")       // true （不可轉換為數字）
    isNaN(true)         // false（可以轉換為數字1。Number(true) = 1）
  ```

**[ 數值轉換： Number()、parseInt() 和 parseFloat() ]**

- **Number() 方法**

```javascript

Number(true)        // 1  （Boolean值，true轉換1，false轉換為0）

Number(5)         // 5  （數字值，直接返回）

Number(null)        // 0  （null值轉換為0）
Number(undefined)     // NaN（undefined值轉換為NaN）

Number("123")       // 123（字符串中只包含數字）
Number("00011")     // 11 （前導的0會被忽略）

Number("")          // 0  （空字符串轉換為0）
Number("hello")     // NaN（字符串中沒有上述格式字符，轉換為NaN）

```

- **parseInt() 方法**

不指定基數意味著讓 parseInt() 決定如何解析輸入的字符串，為了避免錯誤的解析，建議始終將10作為第二個參數（因為多數情況下要解釋的都是10進制數值）。

如： `parseInt(22.5, 10)`

```javascript

// parseInt()方法會忽略字符串開頭的空格，直到找到第一個非空格字符。
parseInt("1234")        // 1234
parseInt(" 1234")       // 1234
parseInt("   1234")     // 1234
parseInt("0001234")     // 1234

// 如果第一個字符是數字字符，它會繼續往後解析，直到解析完成或遇到非數字字符。
parseInt("1234blue")      // 1234

// 如果第一個字符為 非數字字符 或 空字符串，parseInt() 返回NaN。
parseInt("blue1234")      // NaN
parseInt("blue")        // NaN
parseInt("")          // NaN

// "22.5被轉換為22，因為小數點不是有效數字字符"
parseInt(22.5)          // 22

```

- **parseFloat() 方法**

parseFloat() 只解析10進制，所以沒有第二參數指定基數的用法

```javascript

// parseFloat()方法會忽略字符串開頭的空格和前導字符0，直到找到第一個無效的浮點數字字符。
 parseFloat("22.5")       // 22.5
 parseFloat("0022.5")       // 22.5
 parseFloat("22.34.5")      // 22.34 (第一個小數點是有效的，但第二個就是無效的了)
 parseFloat("22")         // 22 (沒有小數點，返回整數)
 parseFloat("22.000")       // 22 (小數點后都為0，返回整數)

```

------

### String

 - toString() 方法

 Number，Boolean，String，object都有toString() 方法

 ```javascript

  var num = 11;
  num.toString()        // "11"

  var found = true;
  found.toString()      // "true"

  var str = "test"
  str.toString()        // "test"（返回自身）

  var obj = {}
  obj.toString()        // "[object Object]"

 ```

 - String() 方法

 在不知道要轉換的值是否null或undefined的情況下，可以使用String() 方法。它可以將任何類型的值轉換為字符串。

 ```javascript

  String(10)            // "10" （有toString() 方法的，調用此方法并返回結果）
  String(null)          // "null"
  String(undefined)     // "undefined"

 ```








