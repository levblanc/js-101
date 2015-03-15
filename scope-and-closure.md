## Scope 作用域

一個function的作用域，以它的花括號（```{}```）為界。

```javascript
  var add = function(a, b){      // 作用域開始
    return a + b;
  };                             // 作用域結束
``` 

一個function的scope chain，從它自身的作用域開始，一直到global層作用域結束。

它能訪問到scope chain中的所有變量。當在本層的作用域（scope）中找不到指定的變量時，它會繼續向上一層作用域尋找，直到chain結束。

```javascript
  var globalNum = 1;
  
  var sum = function(){
    var localNum = 2;
    
    var add = function(){
      return globalNum + localNum;
    };
    
    return add();
  };
  
  sum();        // 3
  
  // add的scope chain，它能訪問到這條鏈條中的所有變量
  
  . global
  |
  |-- sum
       |
       |-- add

```

## Closure 閉包

下面修改一下剛剛的代碼片段，返回時不直接執行```add```方法：

```javascript
  var globalNum = 1;
  
  var sum = function(){
    var localNum = 2;
    
    var add = function(){
      return globalNum + localNum;
    };
    
    return add;
  };
  
  var localSumGlobal = sum();
  localSumGlobal();                 // 3  

```

從代碼中可以看到，sum方法執行以後，它的```localNum```變量，直到下一行代碼```localSumGlobal()```執行時，依然可以訪問到。

代碼中的```add```方法符合了以下條件：

* 訪問了它外層方法的變量
* 其外層方法執行完畢以後，它還能隨時訪問到外層方法中的變量 

所以通常把這類方法叫做「閉包」。

### 閉包的用處（待完善）

構造對象時，可以保持私有變量。

```javascript
  // factory pattern
  
  var person = function(firstName, lastName){
    var homeLand = "earth";
  
    var message = "Hi, my name is " + firstName + " " + lastName;
    
    return {
      name : function(){
        return firstName + “ ” ＋ lastName;
      },
      greet : function(){
        return message;
      },
      homePlanet : homeLand    
    }
  };
  
  var johnSmith = person("John", "Smith");
  var amyGray = person("Amy", "Gray");
  
  johnSmith.name();      // "John Smith"
  amyGray.name();        // "Amy Gray"
  
  johnSmith.homePlanet;  // "earth"
  amyGray.homePlanet;    // "earth"

```