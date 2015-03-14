## 用到爛，但原來到CSS3才有的樣式

  * ```border-radius```   （IE9）
  * ```box-shadow```      （IE9）
  * ```box-sizing```      （IE8部份支持）
    * border-box
  * ```background-size``` （IE9）
  * ```linear-gradient``` （IE10）
  * ```radial-gradient``` （IE10）
  * ```text-shadow```     （IE10）
  * ```@font-face```      （IE9）
  * ```transform```       （2D, IE9 with prefix '-ms-'）
    * translate()
    * rotate()
    * scale()
  * ```transform```       （3D, IE10）
    * rotateX()
    * rotateY()
    * rotateZ()
  * ```transition```      （IE10）
  * ```@keyframes```      （IE10）
  * ```animation```       （IE10）
  
  常用偽類：
  
  * ```:nth-child(x)```
  * ```:enabled``` / ```:disabled```
  * ```:checked```

  不常用偽類：
  
  * ```:first-of-type``` / ```:last-of-type```
  * ```:only-of-type```
  * ```:only-child```
  

## ```<link>``` 和 ```@import```


```<link>```是HTML標籤，在HTML文件中引入CSS文件。其實就是告訴瀏覽器這個頁面對應的樣式文件是什麼，形成一種HTML和CSS文件的對應關係。一般推薦使用```link```標籤引入CSS文件。 

```@import```是CSS引入機制，在一張CSS中引入另外一張樣式。使用```@import```的其中一個原因，是針對老舊瀏覽器的hack，因為它們不知道```@import```，所以可以用它來隱藏一些樣式（不希望被老舊瀏覽器渲染的CSS，就放在```@import```中引入）。

但是，Steve Souders在 [*don’t use @import*](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/) 一文中，詳細對比了通過```<link>
```和```@import```來引入CSS的性能差異。

如果是在HTML文件的```<head>```部份，通過```<link>```標籤引入多個CSS文件，這些文件會在保持引入順序的同時，並行載入。

但如果通過```@import```方式，無論是在```<head>```部份引入，還是在CSS文件引入，這些引入的文件都是按順序逐個載入的。

所以正如文章的標題，作者推薦使用```<link>```標籤。

PS：```<link>```的權重高於```@import```。

## 樣式優先級順序

### 層疊順序（從小到大）
1. User agent declarations
2. User declarations,
3. Author declarations,
4. Author ```!important``` declarations,
5. User ```!important``` declarations

### 樣式權重

|              樣式類型                    |   權重    |
|:---------------------------------------|:----------|
|inline style                            | 1000      |
|ID                                      | 100       |
|class & pseudo-class (```:hover```)     | 10        |
|attribute (```[type="text"]```)         | 10        |
|element & pseudo-element (```:before```)| 1         | 

### 可繼承的樣式（待完善）
  * ```font-family```
  * ```font-size```
  * ```color```

### 不可繼承的樣式（待完善）
  * ```width```
  * ```height```
  * ```padding```
  * ```margin```

## CSS Hacks
```css
 .foo {
    color  : green; /* IE6, IE7, IE8 */
    *color : green; /* IE6, IE7 */
    _color : green; /* IE6 */
 }
```
## Float 元素浮動

設置了浮動的元素，會浮動至容器的左側或右側（根據設置的值）。Float只能設置```left``` 或 ```right```，沒有up或down。

當一個塊狀元素（默認或設置了```display: block;```的元素）設置為float，它後面的元素將會環繞在其周圍。

不同于```absolute```定位，```float```的元素并沒有脫離它本身的流，只是被push到一邊。

### 清除浮動的幾種方式（ 更詳細的講解，可參考文章 [*All About Floats*](https://css-tricks.com/all-about-floats/) ）

 * 當前兩個元素都設置了浮動，第三個元素沒有設置浮動時，會出現如下情況：

 ![float-not-cleared](https://github.com/levblanc/js-101/blob/master/img/float-not-cleared.jpg)
 
 此時可用```clear```來解決
 
 ```css
   .footer {
       clear : both;
   }
 ```
 ![float-not-cleared](https://github.com/levblanc/js-101/blob/master/img/float-cleared.jpg)
 
 * 當container內的所有子元素都設置了float，container會collapse（沒有了高度），如下圖：
 
 ![parent-collapsed](https://github.com/levblanc/js-101/blob/master/img/parent-collapsed.jpg)
 
  此時可用```clearfix```方法來解決
 
 ```css
   .clearfix:after {
       content : '.';
       visibility : hidden;
       display : block;
       height : 0;
       clear : both;
   }
 ```

