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

### 元素權重

|              元素                       |   權重    |
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