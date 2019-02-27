`vua` 支持动态主题色变更，主要是使用 css 变量来制作主题色


css变量简介：

- 2017年3月，微软宣布 Edge 浏览器将支持 CSS 变量。这个重要的 CSS 新功能，所有主要浏览器已经都支持了。

- 声明css变量的时候，变量名前面要加两根连词线（--）。变量名大小写敏感，--header-color和--Header-Color是两个不同变量。

- var()函数用于读取变量。var()函数还可以使用第二个参数，表示变量的默认值。如果该变量不存在，就会使用这个默认值。第二个参数不处理内部的逗号或空格，都视作参数的一部分。

```css
.foo {
  --gap: 20;
  /* 无效 */
  margin-top: var(--gap)px;
}
.foo {
  --gap: 20;
  /* 有效 */
  margin-top: calc(var(--gap) * 1px);
}

```


主题色内置css变量:

`--[primary|secondary|success|info|warning|error]-[lighten|darken]-number`

共 `6 * 10 = 60` 种 