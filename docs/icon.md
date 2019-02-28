`vua` 使用`ant-design`老版图标， 默认连接到 *https://at.alicdn.com/t/font_148784_v4ggb6wrjmkotj4i*;
如果存在网络问题， 可以使用本地资源：

```css
    @font-face {
        font-family: 'anticon';
        font-display: fallback;
        src: url('~vua/src/style/fonts/font_icons.woff') format('woff'),
             url('~vua/src/style/fonts/font_icons.tff') format('truetype'),
    }
```