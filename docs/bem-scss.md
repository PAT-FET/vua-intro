基于scss封装的bem风格：

使用方式如下：
```css
    @include b(v-button){
        @include m(dark){
            color: black;
            @include e(text){
                color: white;
            }
        }
        @include e(text){
            color: #000;
            @include m(primary){
                color: red;
            }
        }
    }
```

编译结果如下：

```css
    .v-button--dark {
        color: black;
    }
    .v-button--dark .v-button__text {
        color: white;
    }

    .v-button__text {
        color: #000;
    }
    .v-button__text--primary {
        color: red;
    }
```