breakpoint in css:

为了方便在css层面使用响应式设计，vua提供了一套mixin用来实现断点样式：(支持自定义断点系统)

```css

@mixin breakpoint-up($name, $breakpoints: $grid-breakpoints);

@mixin breakpoint-down($name, $breakpoints: $grid-breakpoints);

@mixin breakpoint-between($lower, $upper, $breakpoints: $grid-breakpoints);

@mixin breakpoint-only($name, $breakpoints: $grid-breakpoints);

```

在css辅助类中， 也融入了断点系统， 比如：


```css
.text-[breakpoint]-center

.m-t-[breakpoint]-2

```