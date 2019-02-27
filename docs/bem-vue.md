bem在vue组件中的使用：

bem实现：

```js
  b (block?: string): string {
    if (block) return hyphenate(block)
    if (this.$options.name) return hyphenate(this.$options.name)
    throw new Error('bem: component name required')
  }

  e (ele: string, block?: string): string {
    return this.b(block) + '__' + ele
  }

  m (modifier: string, ele?: string, block?: string): string {
    if (ele) return this.e(ele, block) + '--' + modifier
    return this.b(block) + '--' + modifier
  }
```

* 注： 块名默认使用组件$option.name

```js
@Component({
  components: {
  },
  name: 'v-tag'
  })
```

在html模版中使用：

```html
<div :class="[b(), typeCls, shapeCls]" :style="[colorStyle]">
  <slot></slot>
  <span :class="[e('close')]" v-if="closable" @click="close()"><i class="anticon anticon-close"></i></span>
</div>
```