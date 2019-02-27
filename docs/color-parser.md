`vua` 提供了颜色解析器(Colorable.ts), 能对 `（主题色|内置色|十六进制颜色)-[暖|冷]-[index] ` 格式进行解析， 方便组件定义颜色。


以Mixins的形式提供：

```js
parseColor (color: string): string {
    if (!color) return ''
    let [prefix, suffix] = sepColor()
    if (prefix.startsWith('#')) {
      return parse(prefix, suffix)
    }
    if (prefix === 'grey') {
      return suffix ? (greyGradation as any)[suffix] : greyGradation['base']
    }
    let bc = (buildinColor as any)[prefix] || ''
    if (bc) {
      return parse(bc, suffix)
    }
    let theme = (this.$vua.theme as any)[prefix]
    if (theme) {
      if (theme.startsWith('#')) {
        return parse(theme, suffix)
      }
      if (theme === 'grey') {
        return suffix ? (greyGradation as any)[suffix] : greyGradation['base']
      }
      let bc = (buildinColor as any)[theme] || ''
      if (bc) {
        return parse(bc, suffix)
      }
    }
    return color

    function sepColor (): string[] {
      let suffix = ''
      let prefix = color
      let idx = color.indexOf('-')
      if (idx !== -1) {
        prefix = color.substring(0, idx)
        suffix = color.substr(idx + 1)
      }
      return [prefix, suffix]
    }

    function parse (prefix: string, suffix: string) {
      if (suffix) {
        return colorPalette(prefix, gradationMap[suffix])
      }
      return prefix
    }
  }
```

