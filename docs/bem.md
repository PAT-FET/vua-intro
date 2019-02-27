- BEM的意思就是块（block）、元素（element）、修饰符（modifier）,是由Yandex团队提出的一种前端命名方法论。这种巧妙的命名方法让你的CSS类对其他开发者来说更加透明而且更有意义。BEM命名约定更加严格，而且包含更多的信息，它们用于一个团队开发一个耗时的大项目。

- 命名约定的模式如下：

```css
.block{}
.block__element{}
.block--modifier{}

```


- .block 代表了更高级别的抽象或组件。
- .block__element 代表.block的后代，用于形成一个完整的.block的整体。
- .block--modifier代表.block的不同状态或不同版本。