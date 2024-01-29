# section2 @use - Introduction

來看一下另一個 sass 模組化的語法 `@use`

## source code

檔案結構
```bash
.
├── _mixins.scss
├── _variables.scss
└── style.scss
```

```scss
/* style.scss */
@use "./_variables.scss";
@use "./_mixins.scss";

div {
  color: variables.$primary;
  @include mixins.h1;
  .box {
    background: variables.$secondary;
    @include mixins.h2;
  }
}
```

檔案結構跟 sec1 的 `@import` 一樣，但是變數的使用方式不一樣，`@import` 是直接使用變數名稱，`@use` 則有 scope 的概念，必須要加上前綴 `檔名.變數名稱`。

## compile

dist 目錄結構
```bash
.
└── style.css
```

```css
/* style.css */
div {
  color: #007bff;
  font-size: 2rem;
  color: red;
}
div .box {
  background: #6c757d;
  font-size: 1.5rem;
  color: blue;
}
```

可以看到跟 sec1 的結果一樣


## 小結
1. `@use` 跟 `@import` 一樣都可以在編譯的時候引用其他 scss 檔案，並且將其內容合併到當前檔案中。
2. `@use` 有 scope 的概念，必須要加上前綴 `檔名.變數名稱`。