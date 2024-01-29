# section 3 nest - @use and @forward

呈上一個小節的問題，如果我們想要用建立一個單一入口的檔案，讓所有的變數都可以在這個檔案中使用，該怎麼做呢？

```scss
/* style.scss */
@use "./lightColors";

div {
  color: lightColors.$primary;
  background-color: lightColors.$primary-light;
  .box {
    background-color: lightColors.$secondary-light;
  }
}
```

## 改寫檔案

```scss
/* lightColors.scss */
@use "./constant/defaultColors";
@forward "./constant/defaultColors";

$primary-light: lighten(defaultColors.$primary, 30%);
$secondary-light: lighten(defaultColors.$secondary, 30%);
$success-light: lighten(defaultColors.$success, 30%);
$info-light: lighten(defaultColors.$info, 30%);
$warning-light: lighten(defaultColors.$warning, 30%);
$danger-light: lighten(defaultColors.$danger, 30%);
```

透過 `@forward` 我們可以將 `defaultColors` 的變數匯出，讓 `style.scss` 可以使用，類似 `export` 的概念。

## 小結
- 透過 `@use` `@forward` 的搭配，可以讓我們建立類似 `@import` 的檔案結構，但是又保持 `@use` 的優點