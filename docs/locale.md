`vua` 目前支持两种语言（中文与英文）

关于国际化有种不同的使用场景：

1. 切换语言包
2. 组件级别的国际化


导入语言包， 使用内置的或则自行提供：

```js
import zhHans from 'vua/src/locale/zh-Hans'

Vue.use(vua, {
    lang: {
        locales: {'zh-Hans': zhHans},
        current: 'zh-Hans'
    }
})
```

任何具有国际化的组件都提供了`locale`属性， 可使用该属性实现组件的国际化

```js

<template>
<div>
   <div class="my-3">
      <v-popconfirm :cancel-fn="onCancel" :confirm-fn="onConfirm" :locale="locale" title="Are you sure delete this task?" >
         <a class="text-primary">编辑</a>
      </v-popconfirm>
   </div>
</div>
</template>
<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator'

/**
 * @title  自定义文字内容
 * @desc 提供locale替换文字。
 */
@Component({
  components: {
  },
  })
export default class TextExample extends Vue {
   locale: Record<string, string> = {
      ok: '保存',
      cancel: '撤销'
   }

   onConfirm () {
     this.$message.info('confirm')
   }

   onCancel () {
     this.$message.error('cancel')
   }
}
</script>


```