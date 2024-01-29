# section2 @use - feature

繼續來看一下 @use 還有哪些功能

## private variable

```scss
/* mixins.scss */
// private variables
$_font-size-h1: 1rem;

@mixin h1 {
  font-size: $_font-size-h1;
  color: red;
}

```

```scss
/* style.scss */
@use "./_mixins.scss";

div {
  font-size: mixins.$_font-size-h1; // Error: no variable $_font-size-h1 found.
}
```

```scss
/* style.scss */
@use "./_mixins.scss";

div {
  @include mixins.h1;
}
```

可以看到在 style.scss 中無法使用 `_mixins.scss` 中的 private variable，但是可以使用 `_mixins.scss` 中的 mixin。

## namespace

```scss
/* style.scss */
@use "./_variables.scss" as color;

div {
  color: color.$primary;
}
```

重新命名 `_variables.scss` 的 namespace

## configuration

```scss
/* border.scss */
// configuration ans private variables
$_border-width: 1px !default;
$_border-color: #ccc !default;
$_border-style: solid !default;

@mixin border {
  border: $_border-width $_border-style $_border-color;
}
```

正常使用

```scss
/* style.scss */
@use "./_border.scss";

div {
  @include border.border;
}
```

```css
/* style.css */
div {
  border: 1px solid #ccc;
}
```

複寫預設值

```scss
/* style.scss */
@use "./_border.scss" with (
  $_border-width: 2px,
  $_border-color: red
);

div {
  @include border.border;
}
```

```css
/* style.css */
div {
  border: 2px solid red;
}
```

可以在 `border.scss` 中設定預設值，並且在 `style.scss` 中覆寫預設值。

## 小結
1. 變數可以使用 `$_` 來設定 private variable
2. `@use` 可以使用 `as` 重新命名 namespace
3. `@use` 可以使用 `with` 複寫預設值