## W3C標準

> 網頁標準（或Web標準）一般是指有關於WWW各個方面的定義和說明的正式標準以及技術規範。近年來，這個術語也時常和一套建立網站的標準化的最佳實踐方法、網頁設計的原理、以及上述方法的衍生物連繫在一起。

> 如果有網站或網頁宣稱遵循網頁標準，通常就表示他們的網頁符合HTML、CSS、JavaScript等標準。HTML的部分也要滿足無障礙性以及HTML語義的要求。
 
> 當談及網頁標準時，下列各項一般也會被視為基本要素︰
>
  * W3C所推薦的標記語言，例如HTML、XHTML、SVG、XForms。
  * W3C所推薦的樣式表，特別是CSS。
  * Ecma國際所制訂的ECMAScript標準，它是一種更為通用的JavaScript。
  * W3C所推薦的DOM。
  * 對於從URI參考的網頁以及各種資源都要有格式正確的名稱和位址，這部分應以IETF的RFC 2396為基準。
  * 傳送頁面、傳回資料或請求其它的資源時，須正確的使用HTTP和MIME，這部分應以IETF的RFC 2616為基準。
  
> from: [*Wikipedia 網頁標準*](http://zh.wikipedia.org/zh-hk/%E7%B6%B2%E9%A0%81%E6%A8%99%E6%BA%96)

## 各瀏覽器的渲染引擎

  * Internet Explorer : Trident
  * Firefox : Gecko
  * Safari : WebKit
  * Chrome and Opera (from version 15) : Blink，WebKit的分支。

## Semantic HTML 語義化的HTML

語義化的標籤，僅從字面上，就可以清楚地向瀏覽器和開發者描述它自身的意思。

通常是簡單的單詞（如```<header>```），或者被廣泛接受的單詞縮寫（如```<nav>```）。

> A semantic element clearly describes its meaning to both the browser and the developer.    
 from: [*HTML5 Semantic Elements*](http://www.w3schools.com/html/html5_semantic_elements.asp)
 
```<div>```、```<span>```、```<p>``` 等標籤，從字面上是很難看出它的意思的。
```<header>```、```<article>```、```<footer>``` 這些HTML5標籤所表達的意思，就很直觀了。

HTML5新提供的語義化標籤有：

  * ```<header>```
  * ```<nav>```
  * ```<section>```
  * ```<aside>```
  * ```<article>```
  * ```<summary>```
  * ```<main>```
  * ```<mark>```    （用黃色背景色高亮文字）
  * ```<details>``` （會生成可展開的Details列表）
  * ```<figure>```
  * ```<figcaption>```
  * ```<audio>```
  * ```<video>```   （有默認寬高）
  * ```<canvas>``` 
  * ```<time>```
  * 等等……

## 關於<!DOCTYPE>聲明

> 這一部份的內容來自 [*HTML <!DOCTYPE> Declaration*](http://www.w3schools.com/tags/tag_DOCTYPE.asp)


### 定義及使用方法
<!DOCTYPE>聲明不是HTML標籤。它必須寫在HTML文檔第一行，<html>標籤之前。

<!DOCTYPE>告訴瀏覽器，該頁面是用哪個HTML版本進行編寫。

在HTML4.01中，<!DOCTYPE>聲明引用DTD（Document Type Definition），因為HTML4.01基於[SMGL](http://en.wikipedia.org/wiki/Standard_Generalized_Markup_Language)。DTD列明了標記語言規則，讓瀏覽器可以正確渲染頁面內容。

HTML5不基於SMGL，因此不需要引用DTD。

### HTML4.01 和 HTML5的差異
HTML4.01有三種不同的<!DOCTYPE>聲明方式，而HTML5僅有一種。例子如下：

####HTML5

```html
  <!DOCTYPE html>
```

#### HTML4.01 Strict（嚴格模式）

該DTD包含所有HTML元素和屬性，但**不包括**展示性的（presentational）或已棄用的（deprecated）元素（如```<font>```）。不允許使用framesets。

```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

#### HTML4.01 Transitional（過渡模式）

該DTD包含所有HTML元素和屬性，**包括**展示性和已棄用的元素。不允許使用framesets。

```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
```

#### HTML4.01 Frameset 

該DTD與HTML4.01 Transitional相同，但允許使用frameset。

```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
```

### 怪異模式和標準模式

W3C標準出現后，瀏覽器引進兩套模式，分別用於兼容之前已存在的網頁，以及正常顯示按照W3C標準寫成的新網頁。
> In the old days of the web, pages were typically written in two versions: One for Netscape Navigator, and one for Microsoft Internet Explorer. When the web standards were made at W3C, browsers could not just start using them, as doing so would break most existing sites on the web. Browsers therefore introduced two modes to treat new standards compliant sites differently from old legacy sites.

> from: [*Quirks Mode and Standards Mode*](https://developer.mozilla.org/en-US/docs/Quirks_Mode_and_Standards_Mode)

如今，瀏覽器的layout engine有三種可使用的模式：quirks mode, almost standards mode, 和 full standards mode。

  * quirks mode：模仿Navigator 4及Internet Explorer 5上的非標準行為
  * almost standards mode：僅有非常少怪異（quirks）行為會生效
  * full standards mode：遵循HTML和CSS標準的行為

如果HTML文檔的第一行不是<!DOCTYPE>聲明，即使你僅僅是寫了一行註釋，都會觸發quirks mode。

關於不同瀏覽器如何觸發不同模式，可以參閱 [Activating Browser Modes with Doctype](https://hsivonen.fi/doctype/)