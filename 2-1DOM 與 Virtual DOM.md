#DOM  #virtualDOM 

！！在瀏覽器中 #DOM 和瀏覽器的畫面渲染引擎綁定，因此操作 DOM 就會連動更新畫面繪製結果

使用現代前端框架，如： #React , #Vue  在多數情況下，是不用直接對 DOM 本身操作
操作 DOM 的行為，則有現代框架作為代理處理


# DOM (Document Object Model)
1. **樹狀結構**
	- DOM 是一種樹狀資料結構，用來表示瀏覽器中的畫面結構
	- DOM 當中包含==整個畫面元素== ，一個元素就是一個 DOM element
2. **語言獨立**：雖然常與 JavaScript 一起使用，但 DOM 可以被任何程式語言使用。
3. **動態互動**
	- 通過 DOM，腳本可以動態地讀取、增加、刪除或修改頁面的元素和屬性
	- DOM element 是瀏覽器內建特殊  #JavaScript 元件，包含該元素的屬性及相關操作方法

## DOM 及 渲染引擎關聯性
1. **DOM 的角色**：DOM 提供了一個 #樹狀結構 的模型，它表示了網頁的內容結構。當你的網頁加載時，瀏覽器會解析 HTML 文件，並將其轉換成 DOM 結構。這個結構允許開發者通過腳本語言（如 JavaScript）來訪問和操作網頁的各個部分。
2. **瀏覽器渲染引擎**：瀏覽器的渲染引擎則負責將 DOM 和 CSS（層疊樣式表）轉化為用戶能看到和與之互動的視覺表示。它基本上是將代碼和指令轉化為圖形界面。    
3. **互動性**：當開發者使用 JavaScript 等語言操作 DOM 時，比如更改元素的內容、添加或刪除元素，這些改變會被瀏覽器的渲染引擎捕獲。然後，渲染引擎會根據這些變化重新渲染頁面或頁面的一部分。這個過程稱為“重繪”和“重排”。
4. **性能考慮**：
	- 當我們對 DOM 進行操作時，渲染引擎會自動進行一系列更新過程
	- 由於 DOM 操作可能會導致頁面重繪，過度或不當的 DOM 操作可能會對網頁性能產生負面影響。
	- 在大型或複雜的網頁中，不斷的 DOM 操作可能導致界面顯著的卡頓或延遲。

> 以最小的範圍的 DOM 操作來完成所需的畫面變更

> 當我們對 DOM 進行操作時，渲染引擎會自動進行一系列更新過程


[MDN - DOM](https://developer.mozilla.org/zh-TW/docs/Web/API/Document_Object_Model)
# Virtual DOM
[[How Does React Actually Work ?#virtual DOM]]
Virtual Dom 是一種為了提升畫面處理效能，而產生的程式設計概念，每一個前端框架在實作上略有差異，但核心概念是模擬實際的DOM 而產生的虛擬資料結構。

通常以Virtual DOM 概念所實現的『虛擬畫面資料結構』會是一種模擬並描述實際DOM 結構資料。

在 #react 中，Virtual DOM 跟 實際 DOM 的關係，是先有 Virtual DOM 才有 DOM。
兩者同步化關係是，Virtual DOM => DOM 單向


## 畫面更新策略

Virtual DOM 可以想像為模擬用試作品。當首次繪製時，會產生一份 Virtual DOM 結構，且轉換出對應的實際 DOM 結構。

當 UI 有更新時，會進行以下：
1. 產生新的 Virtual DOM 作為新的試做品
2. 比較新與舊的Virtual DOM 做出需要操作的差異 (diff)
3. 根據差異執行最小化的 DOM 操作

---

不划算
- 前後產生的 react element 是一樣
		- setState(1) 和 1 一樣
- 比較後重繪制
- 人工操作不會造成完美


virtual Dom vs 人工操作 dom