[toc]

# React 시작 및 환경세팅

---

## JS로 시작하기

```js
npx create-react-app 레포명
```



## 타입스크립트로 시작하기

```js
npx create-react-app 레포명 --template typescript
```



## react-router-dom 설치

1. js설치

```js
npm i react-router-dom
```

2. 타입스크립트로 설치

```js
npm i react-rouer-dom @types/react-router-dom
```



## 리덕스 설치

1. JS설치

```js
npm i redux react-redux
```

2. 타입스크립트 설치

```js
npm i redux react-redux @types/react-redux
```



리덕스 폴더구조

---

src
	config
		configStore.ts
	modules

---



## TailWindCss 설치

```js
npm i -D tailwindcss postcss autoprefixer
npx tailwindcss init
```

### tailwind.config.js설정

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{html,js,tsx,ts}"],
  theme: {
    extend: {
      colors: {
        primary: "#21BF48",
        mainText: "#000000",
        subText: "#767676",
        accentText: "#EB5757",
        background: "#f2f2f2",
      },
      fontSize: {},
      fontFamily: {},
    },
    screens: {
      ss: "480px",
      sm: "620px",
      sl: "768px",
      md: "1060px",
      lg: "1200px",
    },
  },
  plugins: [],
};

```

### 최상위 루트 CSS파일에 Tailwind적용

src/index.css

```css
/** index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```



## NodeMon 설치

npm i nodemon
