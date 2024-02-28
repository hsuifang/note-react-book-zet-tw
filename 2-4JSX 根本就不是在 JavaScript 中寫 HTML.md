#讀書會  #TechBookCommunity

> React element 是在 React 中作為畫面結構描述的最小單位。

React element 可以透過 `createElement` 方法建立，並透過 `react-dom`的處理後，產生實際的 DOM element。
但多數的專案，卻不常見到 createElement ，而是長得像 HTML 的 #JSX 的語法。


# 什麼是 JSX 語法
雖然能透過 `createElement` 建立 React Element 定義預期畫面，但為了能較為符合以往撰寫HTML的開發體驗，React 提供了 #JSX 的語法糖，能讓我們在建立 React Element 時，有著類似撰寫 HTML 語法的體驗。

> 也就是說 JSX 為什麼跟HTML 這麼相像，是刻意而為之

透過特定的轉譯工具，即會讓JSX 轉變成 React.createElement的樣貌，也就是說**撰寫 JSX 語法即是在寫 React.createElement的呼叫**。


## 對比 React.createElement 及 JSX

Dom element 最終如果要產生
``` HTML
<div id="wrapper">
	<ul>
		<li>a</li>
		<li>b</li>
	</ul>
	<button>dddd</button>
<div>
```

### React.createElement
```js
const reactElement = React.createElement(
  "div", 
  { id: "wrapper" },
  React.createElement(
    "ul",
    null,
    React.createElement("li", null, "a"),
    React.createElement("li", null, "b")
  ),
  React.createElement(
    "button",
    null,
    "dddd"
  )
);
```

### JSX
```jsx
const reactElement = (
	<div id="wrapper">
		<ul>
			<li>a</li>
			<li>b</li>
		</ul>
		<button>dddd</button>
	<div>
)
```

註記： JSX 搭配轉譯工具即會同於 React.createElement 寫法

# 如何讓 JSX 在 瀏覽器運行
若要將 JSX 語法在一般的 JavaScript 執行環境中正常運作，需要透過一些轉譯工具。
而 JavaScript 中最主流的轉譯工具 : Babel

## 轉譯工具 - Babel
Babel 是 JavaScript 社群中主流的 source code transpiler，其可以將原始碼轉譯成另一種模樣的 JavaScript

Babel 在 JavaScript 的運用廣泛，例如：

- 將 ECMAScirpt 的語法轉譯成邏輯相同的舊版語法，達到相容於舊的瀏覽器
- JSX transformer  - JSX 語法轉換成 React.createElement的轉換工具
- 自定義語法轉譯

## JSX  transformer
一般的瀏覽器並不能直接支援解讀JSX 語法，若要執行程式原始碼，需要將 JSX 語法都轉成使用 React.createElement 方法呼叫的樣貌，最終以轉譯後的版本在瀏覽器執行

轉譯JSX 語法的工具稱作 **「JSX transformer」**，有各式各樣的 JSX transformer 在社群中，其中以 Babel 之的的 transpiler 較為熱門，同時也是官方合作方案。


- 以 `create-react-app` 可以見到 `@babel/preset/react`， 其中以 `@babel/plugin-transform-react-jsx` 進行轉譯
- 以 `vite` 建置 react 選擇 `JavaScript` 可以見到 `@vitejs/plugin-react` ，其中以`@babel/plugin-transform-react-jsx-self` 進行轉譯
- 以 `vite` 建置 react 選擇 `JavaScript + swc` 可以見到 `@vitejs/plugin-react-swc` 組合包，搭配 `jsx runtime` 進行轉譯。 [github](https://github.com/vitejs/vite-plugin-react-swc)

### 程式碼在 build time 時的靜態處理
轉譯的行為是發生在 開發環境中的 `建置階段`，而非在瀏覽器的執行階段。

> React 專案中的 HTML 引入的 JavaScript 檔案的內容是 Babel 轉譯後的原始碼

以實際的開發流程，在每次存擋中，轉譯工具就會自動重新執行轉譯行為，並產生對應程式碼。這種流程被稱為程式碼的靜態分析與處理，所謂==靜態==是指尚未執行程式碼時，先以純文字形式對程式碼的語意、結構和行為進行分析，再執行相關轉譯、檢查以及優化。

#### Babel 轉譯 JSX 流程：
- 撰寫 JSX 語法
- 在 build time，經過 Babel 轉譯 JSX 語法，產生output.js 檔案
- 在 runtime 時讀引入Babel 執行後的 output.js

### 新版的 JSX transformer 與 jsx-runtime
在 React 17 (<=16 )以前，若沒有在 JS 檔案中寫 `import React form 'react'`會發生`React is not found`錯誤 ，
這是轉譯機制白紙黑字輸出的問題。

React 17 開始 ， 透過Babel 新的 JSX transformer 以及 React 17 開始 支援 `jsx-runtime`，帶來以下好處：
- 不再需要為了使用 JSX 語法而引用 React
- 改善 bundle 大小
- 效能與提示優化
- 新舊 transformer 的 JSX 語法上完全相容


> 新版有別於舊版不會將 JSX 語法轉譯成 `React.creactElement`，而是改成 React 17 所提供 jsx-runtime 的 `_jsx` 方法，但實際最終都是產生 React element


# 其他 
## 常見誤會
### JSX 屬性命名規定
- JSX 要將class 的 屬性寫成 className 是因為 **React element 對於屬性命名的規定**，而非JSX 語法要求

## 章節檢測
**JSX 語法的用途是什麼？其背後的本質為何？** 
JSX 是一種語法糖，它讓開發者以一個更好的開發體驗來定義並建立建立 React Element

**JSX 語法為什麼長得很像 HTML 語法？** 
是刻意被設計成這樣，他的本質就是是建立 React Element，而不是 HTML 或 DOM element

**開發時撰寫的 JSX 語法是透過哪些流程處裡，最後才能順利的在瀏覽器中執行並定義畫面的？**
在 build time 時透過 transformer 轉換成 `React.createElement()` 或 `_jsx()`的呼叫語法，並產生 output.js 檔案，在 runtime 時引用 `output.js` ，並將 React element 轉換為 DOM element 注入到指定的容器中