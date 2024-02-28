#React 
# What is React Element?
React 是基於 Virtual DOM 的設計模式實作一套 UI 機制
Virtual DOM 畫面結構裡的每個元素被稱作 「React Element」，作為描述、組成畫面的最小單位。

> **React Element 是 React 基於 Virtual DOM概念所實現的==虛擬畫面結構元素==**，因此他是一種 JavaScript 的物件資料，用來描述預期的的實際 DOM element 結構。

# 如何建立
Sample :::  [[Pure React & CreateElement]]
可以透過 React 提供 `createElement` 的方法建立一個 React Element，而實際最終產出的 DOM 同於描述檔案。

## 使用 createElement
```js 
import React from 'react'
const buttonReactElement = React.createElement(
	'button',            // 元素類型
	 { type: 'button' },  // 屬性
	 'Click me!'     // 子元素
)
```

第一個參數為元素類型，第二個參數為屬性，而第三個參數則為子元素。
與實際的 DOM element一樣， React element 也可以是巢狀的樹狀結構，一個 React Element 也可以是另一個 React Element 的子元素

## react element - JS 物件資料
```js
{
 type: "button",
 key: null,
 ref: null,
 props: {
	 type: "button",
	 children: "click me!"
 },
 $$typeof: Symbol(react.element),
}

```

React Element / Virtual DOM / DOM


# !! 注意
## 建立後，不能被修改
在 React 實作 Virtual DOM概念就是 `React element`，他是在描述某個時間點版本的畫面結構。
而 React 更新、操作 DOM 的機制是透過比較新舊的 Virtual DOM，所以一但可以修改歷史紀錄，比較機制就會毀了

## React Element 與 DOM Element 的差異
React Element 的屬性名稱和格式，與 DOM element 略有差異

### 大部分屬性名稱以 Camel Case 命名
- onclick => onClick，tabindex => tabIndex
- `aria-*` 和 `data-*` 則維持

### 保留字會改變名城
- className
- htmlFor

### Style 內容格式
- 在 React Element 用 物件表示
