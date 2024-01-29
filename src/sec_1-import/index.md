# section 1 - @import

複習一下 sass 模組化的基礎 `@import`

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
@import "./_variables.scss";
@import "./_mixins.scss";

div {
  color: $primary;
  @include h1;
  .box {
    background: $secondary;
    @include h2;
  }
}
```

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

## 小結
1. `@import` 可以在編譯的時候引用其他 scss 檔案，並且將其內容合併到當前檔案中。
2. 檔名前綴 `_*.scss`，不會被編譯成 css 檔案。
