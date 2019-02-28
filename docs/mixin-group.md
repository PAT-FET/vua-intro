分组 mixin (Group.ts  Groupable.ts)

    组件在创建时会自动加入组， 销毁时自动移除组， 并支持嵌套


- Group
    - `groupNames` - 指定组成员名， 不指定默认所有`Groupable`


```js
import Vue from 'vue'
import Component from 'vue-class-component'
import { Provide } from 'vue-property-decorator'
import Groupable from './Groupable'

@Component
export default class Group extends Vue {
  groupNames: string[] = []

  groupItems: Groupable[] = []

  groupNestedLevel: number = 0

  @Provide('addGroupItem') provideAddGroupItem (item: Groupable) {
    if (this.groupNames.length > 0 && !this.groupNames.includes(item.groupName)) return
    if (this.groupItems.includes(item)) return
    this.groupItems.push(item)
  }

  @Provide('removeGroupItem') provideRemoveGroupItem (item: Groupable) {
    let idx = this.groupItems.findIndex(v => v === item)
    if (idx >= 0) this.groupItems.splice(idx, 1)
  }

  @Provide('inGroup') provideInGroup (item: Groupable): boolean {
    return this.groupItems.includes(item)
  }

  @Provide('groupNestedLevel') provideGroupNestedLevel (): number {
    return this.groupNestedLevel
  }
}


```


- Groupable
    - groupName - 成员名， 默认组件名

```js
import Vue from 'vue'
import Component from 'vue-class-component'
import { Inject } from 'vue-property-decorator'
import { noop } from '../utils'

@Component
export default class Groupable extends Vue {
  groupName: string = this.$options.name || ''

  groupNestedLevel: number = 0

  @Inject({ from: 'addGroupItem', default: () => noop }) injectAddGroupItem!: (item: Groupable) => void

  @Inject({ from: 'removeGroupItem', default: () => noop }) injectRemoveGroupItem!: (item: Groupable) => void

  @Inject({ from: 'inGroup', default: () => () => false }) injectInGroup!: (item: Groupable) => boolean

  @Inject({ from: 'groupNestedLevel', default: () => () => -1 }) injectGroupNestedLevel!: () => number

  // whether belong to a group
  get grouped (): boolean {
    return this.injectInGroup(this)
  }

  joinGroup () {
    this.injectAddGroupItem(this)
    this.groupNestedLevel = this.injectGroupNestedLevel() + 1
  }

  exitGroup () {
    this.injectRemoveGroupItem(this)
    this.groupNestedLevel = 1
  }

  created () {
    this.joinGroup()
  }

  beforeDestroy () {
    this.exitGroup()
  }
}

```




