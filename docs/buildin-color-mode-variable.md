`vua` 目前提供了 11 种内置黑白变量， 同时提供了相应的scss变量

```css
$heading-color: var(--heading-color); // 标题文字色
$text-color: var(--text-color); // 常规文字色
$text-color-secondary: var(--text-color-secondary); // 辅助文字色
$text-color-active: var(--text-color-active); // 激活文字色
$disabled-color: var(--disabled-color); // 禁用文字色
$bg-color: var(--bg-color); // 背景色
$bg-color-1: var(--bg-color-1); // 选中、 标题头背景色
$bg-color-2: var(--bg-color-2); // 灰色、禁用背景色
$bg-color-active: var(--bg-color-active); // 激活背景色
$border-color-base: var(--border-color-base); // 边框色
$border-color-split: var(--border-color-split); // 分割线色

```


黑白模式下，变量的实际值如下：

```js

const themeLight = {
  '--heading-color': 'rgba(0, 0, 0, .85)',
  '--text-color': 'rgba(0, 0, 0, .65)',
  '--text-color-active': 'var(--primary-base)', // text active
  '--text-color-secondary': 'rgba(0, 0, 0, .45)',
  '--disabled-color': 'rgba(0, 0, 0, .25)',
  '--bg-color': greyGradation['lighten-5'],
  '--bg-color-1': greyGradation['lighten-4'], // selected item, header
  '--bg-color-2': greyGradation['lighten-3'], // grey disabled
  '--bg-color-active': 'var(--primary-lighten-5)', // bg active
  '--border-color-base': greyGradation['lighten-1'],
  '--border-color-split': greyGradation['lighten-2']
}

const themeDark = {
  '--heading-color': 'rgba(255, 255, 255, 1)',
  '--text-color': 'rgba(255, 255, 255, .85)',
  '--text-color-active': 'var(--primary-lighten-4)', // text active
  '--text-color-secondary': 'rgba(255, 255, 255, .65)',
  '--disabled-color': 'rgba(255, 255, 255, .35)',
  '--bg-color': '#303030',
  '--bg-color-1': '#3d3d3d', // selected item, header
  '--bg-color-2': '#4a4a4a', // grey disabled
  '--bg-color-active': 'var(--primary-darken-4)', // bg active
  '--border-color-base': '#636363',
  '--border-color-split': '#575757'
}

```