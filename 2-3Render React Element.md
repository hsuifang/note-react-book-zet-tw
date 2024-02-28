> Target:::
> 1. 如何透過 `react-dom` 來建立 root 並將 React element 繪製成實際 DOM
> 2. React 只會去操作需要真正被更新的 DOM element
> 3. what is reconciler and renderer 的角色與工作，以及 react 也能在瀏覽器以外的環境渲染畫面


# 概念
透過官方所提供的 `react-dom` 將 React element 轉換並繪製成實際的 DOM element，以產生瀏覽器畫面。

## 實作流程
步驟：[[Pure React & CreateElement]]
指定特定區塊，讓React 對其擁有完全的管轄權來持續進行 Virtual DOM => DOM 的單向轉換與同步化

**Step1**:   提供一個輸出實際DOM 結果的目標容器 [[Pure React & CreateElement#建立一個index.html]]
``` html
<body>
	<div id="root"></div>
</body>
```
**Step2:**  建立 ==root== 並指定目標容器
```js
import React from "react";
import ReactDOM from "react-dom/client";

// 實際 DOM 輸出的位置
const container = document.getElementById("root");

// 用此容器作為建立一個 React App 的畫面渲染管轄入口(root) 
const root = ReactDOM.createRoot(container); 

```

**Step3**: 準備 react element
**Step4**: 繪製成實際 DOM element
```js
...
const buttonReactElement = React.createElement(
	"button",
	{ type: "button" },
	"Click me!"
);
...
const root = ReactDOM.createRoot(container); 
root.render(buttonReactElement)
```

# Reconciler & Renderer
在React 的實作設計，負責「定義以及管理畫面結構描述」稱之 #Reconciler ; 而負責將畫面結構的描述繪製成實際畫面成品稱之 #renderer
## Reconciler
- 定義以及管理畫面結構描述
- 在有需要更新時，比較差異處
- [[底層原理#Fiber Reconciler]]
- [[How Does React Actually Work ?#Reconciliation]]

## Renderer
- 將畫面結構繪製成成品
- 用於瀏覽器的 renderer 就是 `react-dom`


----
世界太複雜，當然