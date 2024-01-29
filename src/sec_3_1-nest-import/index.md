# section 3 nest - @import

這一章討論巢狀檔案應該如何處理引入的問題。

## @import

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
@import "./constant/defaultColors";

$primary-light: lighten($primary, 30%);
$secondary-light: lighten($secondary, 30%);
$success-light: lighten($success, 30%);
$info-light: lighten($info, 30%);
$warning-light: lighten($warning, 30%);
$danger-light: lighten($danger, 30%);
```

```scss
/* style.scss */
@import "./lightColors";

div {
  color: $primary;
  background-color: $primary-light;
  .box {
    color: $secondary;
    background-color: $secondary-light;
  }
}
```

使用 `@import` 引入巢狀檔案，所有的變數都會被合併到當前檔案中，等於是全域變數，所以可以在任何地方使用。