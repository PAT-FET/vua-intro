`vua` 支持组件样式动态定制：

允许用户制定的css样式变量定义在组件的`style/var.scss`种： （如： v-menu）

```css
@import "../../../style/var.scss";

$menu-item-height: 2.5rem;
$menu-collapse-width: 5rem;

$menu-base-color: $primary-color;
$menu-hover-color: map-get($primary-colors, lighten-1);

// menu
$menu-bg-color: var(--menu-bg-color, transparent);
$menu-border-color: var(--menu-border-color, #{$border-color-split});

// sub
$menu-sub-title-text-color: var(--menu-sub-title-text-color, #{$text-color});
$menu-sub-title-hover-text-color: var(--menu-sub-title-hover-text-color, #{$menu-hover-color});
$menu-sub-title-active-text-color: var(--menu-sub-title-active-text-color, #{$text-color-active});

// item
$menu-item-text-color: var(--menu-item-text-color, #{$text-color});
$menu-item-hover-text-color: var(--menu-item-hover-text-color, #{$menu-hover-color});
$menu-item-active-text-color: var(--menu-item-active-text-color, #{$text-color-active});
$menu-item-bg-color: var(--menu-item-bg-color, #{$bg-color});
$menu-item-active-bg-color: var(--menu-item-active-bg-color, #{$bg-color-active});
$menu-item-active-border-color: var(--menu-item-active-border-color, #{$text-color-active});
$menu-item-disabled-text-color: var(--menu-item-disabled-text-color, #{$disabled-color});

// group
$menu-group-text-color: var(--menu-group-text-color, #{$text-color-secondary});


```


`vua`提供了`CssVariable`工具来快速重载css样式, 使用方式如下：

用户提供`css-variable`属性， 属性名与相应`var.scss`中名称一致:

```js
<template>
<div>
   <div class="my-3">
      <div class="my-3">
         <v-switch v-model="collapse" inactive-text="收起" active-text="展开"></v-switch>

          <v-radio-group class="ml-3" v-model="mode">
            <v-radio-button label="inline">inline</v-radio-button>
            <v-radio-button label="horizontal">horizontal</v-radio-button>
            <v-radio-button label="vertical">vertical</v-radio-button>
         </v-radio-group>

         <v-radio-group class="ml-3" v-model="trigger">
            <v-radio-button label="hover">hover</v-radio-button>
            <v-radio-button label="click">click</v-radio-button>
         </v-radio-group>
      </div>

      <v-menu :mode="mode"
         :collapse="collapse"
         unique-opened
         :css-variable="cssVariable"
         :trigger="trigger"
         default-active="Mac Book"
         :style="[widthStyle]">
         <v-sub-menu>
            <div slot="title">通讯设备</div>
            <i slot="icon" class="anticon anticon-apple"></i>
            <v-menu-item index="phone" disabled>电话</v-menu-item>
            <v-menu-group>
               <span slot="title">笔记本</span>
               <v-menu-item index="Mac Book">Mac Book</v-menu-item>
               <v-sub-menu>
                  <div slot="title">Mac Pro</div>
                  <v-menu-item index="laptop 2016">2016版</v-menu-item>
                  <v-menu-item index="laptop 2018">2018版</v-menu-item>
               </v-sub-menu>
            </v-menu-group>
            <v-menu-group>
               <span slot="title">手机</span>
               <v-menu-item index="iphone 6">iphone 6</v-menu-item>
               <v-sub-menu disabled>
                  <div slot="title">2018</div>
                  <v-menu-item index="iphone x">iphone x</v-menu-item>
                  <v-menu-item index="iphone 8" disabled>iphone 8</v-menu-item>
               </v-sub-menu>
            </v-menu-group>
         </v-sub-menu>
         <v-menu-item index="dell" disabled>
            <i slot="icon" class="anticon anticon-ie"></i>
            Dell 台式机
         </v-menu-item>
         <v-sub-menu>
            <div slot="title">物理学</div>
            <i slot="icon" class="anticon anticon-chrome"></i>
            <v-menu-item index="quantum" disabled>量子力学</v-menu-item>
            <v-menu-group>
               <span slot="title">经典力学</span>
               <v-menu-item index="Newton">牛顿定律</v-menu-item>
               <v-sub-menu>
                  <div slot="title">刚体运动</div>
                  <v-menu-item index="torque">力矩</v-menu-item>
                  <v-menu-item index="parallel axis theorem">平行轴定理</v-menu-item>
               </v-sub-menu>
            </v-menu-group>
            <v-menu-group>
               <span slot="title">电磁学</span>
               <v-menu-item index="static electricity">静电力</v-menu-item>
               <v-sub-menu disabled>
                  <div slot="title">电与磁</div>
                  <v-menu-item index="amp">安培环路定理</v-menu-item>
                  <v-menu-item index="max" disabled>麦克斯韦方程组</v-menu-item>
               </v-sub-menu>
            </v-menu-group>
         </v-sub-menu>
      </v-menu>
   </div>
</div>
</template>
<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator'
import { MenuCssVariable } from '@/index'

/**
 * @title  自定义主题
 * @desc 自定义主题。
 */
@Component({
  components: {
  },
  })
export default class ThemeExample extends Vue {
   collapse: boolean = false

   mode: string = 'inline'

   trigger: string = 'hover'

   cssVariable: MenuCssVariable = {
      menuBgColor: 'rgb(0, 21, 41)',
      menuBorderColor: 'rgb(0, 21, 41)',
      // group
      menuGroupTextColor: '#999',
      // sub
      menuSubTitleTextColor: 'rgba(255, 255, 255, 0.65)',
      menuSubTitleHoverTextColor: '#fff',
      menuSubTitleActiveTextColor: '#fff',
      // item
      menuItemTextColor: 'rgba(255, 255, 255, 0.65)',
      menuItemDisabledTextColor: '#aaa',
      menuItemHoverTextColor: '#fff',
      menuItemActiveTextColor: '#fff',
      menuItemBgColor: 'rgb(0, 12, 23)',
      menuItemActiveBgColor: 'primary',
      menuItemActiveBorderColor: 'primary'
   }

   get widthStyle () {
     if (this.mode === 'horizontal') return {}
     return {
       width: '256px'
     }
   }
}
</script>

```