## The *this* keyword
JS中的***this***其實跟我們日常用語中的「代詞」很像。

比方說，我們會說，

「小明跑得很快，因為 ***他*** 想要趕上那趟公交。」

其實我們完全可以說，

「小明跑得很快，因為 ***小明*** 想要趕上那趟公交。」

但是在日常用語裡面，我們比較習慣使用「代詞」，

因為這樣避免了名詞重複（啰嗦），同時給了後半句話一個清楚的主語指向。

---
在JS裡面，使用 ***this*** 也是類似的原因。

運行下面這段代碼后，不會出現什麼問題。

```javascript
  var person = {
    name : "John Smith",
    greet : function (){
      return "My name is " + person.name;
    }
  };
  
  person.greet();    // "My name is John Smith"

```

但是，當我們想改變這個object的名字的時候，就會報錯：

```javascript
  var johnSmith = {
    name : "John Smith",
    greet : function (){
      return "My name is " + person.name;
    }
  };
  
  johnSmith.greet();    // Uncaught ReferenceError: person is not defined

```

因為```person```根本沒有定義。只有把```person```修改成```johnSmith```，```name```屬性的指向才是正確的。

也就是說，如果希望指向正確，我們每次都得修改```name```指向的object的名字。如果我定義了100個不同的人，我就得修改100次```name```的指向。

所以，在object的方法中，直接使用object名來獲取其屬性，顯然很麻煩。就像在最開始的句子示例中，一直使用「小明」一樣。

另外有一種情況，就是這個object可能根本沒有名字：

```javascript
  ({
    name : "John Smith",
    greet : function (){
      return "My name is " + person.name;
    }
  }).greet();
  
// Uncaught ReferenceError: person is not defined

```
這個時候，使用 ***this*** 就很直觀方便了。

在下面這段代碼中，***this*** 指的就是```greet```方法所「依附」（attached to）的object。


```javascript
  ({
    name : "John Smith",
    greet : function (){
      return "My name is " + this.name;   // 改為使用this
    }
  }).greet();
  
// "My name is John Smith"

```

現在把最開始的person object修改一下，使用***this***，無論object的名字是什麼，都不會報錯。

```javascript
  var person = {
    name : "John Smith",
    greet : function (){
      return "My name is " + this.name; // person.name改為this.name
    }
  };
  
  person.greet();            // "My name is John Smith"
  
  // 修改object的名字
  var anotherPerson = {
    name : "John Smith",
    greet : function (){
      return "My name is " + this.name; 
    }
  };
  
  anotherPerson.greet();    // "My name is John Smith"

```

最後，是關於「依附」（attached to）的終極解釋。


```javascript
  var name = 'Window Smith';
  
  var greet = function (){
      return "My name is " + this.name; 
    }
  };
  
  var johnSmith = {
    name : "John Smith",
    greet : greet
  };
  
  johnSmith.greet();    // "My name is John Smith"
  greet();              // "My name is Window Smith"

```

當不清楚 ***this*** 的指向的時候，可以問自己一個問題：

「是誰（哪個object）調用了使用***this*** 的方法？」

即

「方法被調用時，***this***所依附的object是哪個？」

答：「```johnSmith``` 和 ```window```。」

(```name```變量和```greet```方法都是global的，他們屬於```window```object。它們其實是```window.name```和```window.greet```)

所以```johnSmith.greet```中的 ***this*** 其實是```johnSmith```的「代詞」，

```this.name``` 也就是 ```johnSmith.name```，即```"John Smith"```。

同理可得，```greet```方法調用時，

```this.name``` 也就是 ```window.name```，即```"Window Smith"```。
