## 什麼是MVC

* **MVC的組成**
  
  * Model：Model是MVC的中心組成部份。它捕捉軟件中其作用范围/與其相關問題（[problem domain](https://en.wikipedia.org/wiki/Problem_domain)）的行為，并不依賴于用戶界面。Model直接管理数据（data）、逻辑（logic）和软件的规则（rules of the application）。
  * View：它可以是任何信息的輸出表現層，例如一個圖表。也有可能是同一個信息的多個視圖，例如一個給管理層用的柱狀圖視圖和一個給會計用的表格視圖。
  * Controller：接收輸入動作(可以理解為“事件”，包括用戶的行为和數據Model上的改變)，并相應轉化為對Model或View的命令。

* **組件之間的互動**
  * Controller可以向Model發出命令來更新Model的`state`。它也可以向其相關的View發出命令，來改變View對Model的展示。
  * Model存儲著Controller拿回來的數據和View展示著的數據。每當數據有改變，都是由Controller更新的。
  * View從Model請求數據來生成面向用戶的表現層。

  組件互動示意圖：
  
  ![mvc-components](https://upload.wikimedia.org/wikipedia/commons/a/a0/MVC-Process.svg)
  
  --
  以上内容翻译和引用自文檔：
  
  1. [MVC](https://zh.wikipedia.org/wiki/MVC). From Wikipedia.
  
  2. [Model–view–controller](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller). From Wikipedia.