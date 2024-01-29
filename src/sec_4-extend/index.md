# section 4 @extend and placeholder

`@extend` placeholder 在 `@use` 引入的時候規則又跟 variable mixin function 不一樣，這裏提醒一下需要特別注意。

```scss
/* style.scss */
@import "_red-color";
@use "_blue-color";

div {
  @extend %red-color;
  // @extend blue-color.%blue-color;
  @extend %blue-color;
}
```

引用 `@extend` placeholder 的時候，`@use` 跟 `@import` 的規則一樣，反而在 scope 沒有。

```scss
/* style.scss */
@import "_red-color";
@use "_blue-color";

div {
  @extend %red-color;
  @extend %blue-color;
  @extend %border
}
```

在巢狀結構的引入 `@use` 跟 `@import` 的規則一樣

## 小結
- 在引用 @extend placeholder 的時候，視同 css 引用。
- 在引用 @extend placeholder 的時候， `@use` 跟 `@import` 的規則一樣