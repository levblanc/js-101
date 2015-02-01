# Javascript Basics
此為個人使用的markdown文檔，用於記錄Javascript的基礎知識。

所列各項均為個人讀書筆記及總結。

2015-02-01 創建


## Data Types

1. 基本數據類型（Primitive Types）

   * Undefined

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
   * Null類型
     
     Null類型同樣只有一個特殊值：*null*。
     
     邏輯上null的值指向一個空對象（empty object pointer），因此使用typeof方法檢測null值時，返回"object"（這個bug有望在ECMAScript 6中修復）。
     
     ```javascript
       var type = null;
       typeof(null);    // "object"
     ```
     
###重點注意事項
     
* *undefined*意為“未賦值”，而*null*意為“已賦值為nothing”。
     
* *undefined*的東西不存在，*null*存在，但真正的值未知。
       
* 這有點像現在與未來。*undefined*是當下，因為我們已經知道它不存在；而*null*則是未來，我們都知道未來存在，只是不知道它的樣子而已。
       
* 留意下文，是‘intentional absence’。所以當定義變量時意在保存object，可以先將其初始化為null。
  > null value: primitive value that represents the intentional absence of any object value ([ECMA-262, 5.1 Edition, 4.3.11](http://www.ecma-international.org/ecma-262/5.1/#sec-4.3.11)).
       
     
* null並不是object，它只是基礎數據類型的一種，你不能給它定義新屬性
       
  ```javascript
  var obj = {};
  null === obj;    // false
  ```     
     

* 既然null不是object，為何typeof方法返回"object"？因為這是規定([The typeof Operator](http://www.ecma-international.org/ecma-262/5.1/#sec-11.4.3))
     
            
   	  
     
