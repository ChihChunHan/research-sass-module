# section 3 nest - @use

## 基本使用

檔案結構
```bash
.
├── constant
│   └── defaultColors.scss
├── lightColors.scss
└── style.scss
```

```scss
/* defaultColors.scss */
$primary: #007bff;
$secondary: #6c757d;
$success: #28a745;
$info: #17a2b8;
$warning: #ffc107;
$danger: #dc3545;
```

```scss
/* lightColors.scss */
@use "./constant/defaultColors";

$primary-light: lighten(defaultColors.$primary, 30%);
$secondary-light: lighten(defaultColors.$secondary, 30%);
$success-light: lighten(defaultColors.$success, 30%);
$info-light: lighten(defaultColors.$info, 30%);
$warning-light: lighten(defaultColors.$warning, 30%);
$danger-light: lighten(defaultColors.$danger, 30%);
```

```scss
/* style.scss */
@use "./lightColors";

div {
  background-color: lightColors.$primary-light;
  .box {
    background-color: lightColors.$secondary-light;
  }
}
```

到這邊，跟前一小節的 @import 沒有太大的差異

## ISSUE

問題來了，如果我們想要在 `style.scss` 中使用 `defaultColors` 的變數，你覺得哪一種寫法比較好？

### 選項A

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

### 選項B

```scss
/* style.scss */
@use "./constant/defaultColors";
@use "./lightColors";

div {
  color: defaultColors.$primary;
  background-color: lightColors.$primary-light;
  .box {
    background-color: lightColors.$secondary-light;
  }
}
```

實際在編譯的時候，選項A會報錯，因為 `defaultColors` 沒有被引入，所以無法使用。選項B則可以正常編譯，但是這樣的寫法在想要讓變數單一進入點的時候，不方便管理。下一個小結會介紹`@forward`，讓我們可以使用選項A的寫法。




