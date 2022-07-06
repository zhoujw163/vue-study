# Vue3使用vite-plugin-vue-setup-extend

>在使用 Vue3.2 的 setup 语法糖后，无法优雅的定义组件的 name 值，虽然 vite 会根据组件的文件名自动生成组件名，但是需要自定义的组件名时，就很不方便。

## 解决方法

**方案1：写两个 script 标签**

```html
<script lang="ts">
export default defineComponent({
    name: 'xxx'
})
</script>    

<script lang="ts" setup>
export default defineComponent({
    name: 'xxx'
})
</script>    
```

这种方法简单，但确实不够优雅

**方案2：使用 vite 插件 vite-plugin-vue-setup-extend**

1. 安装

```shell
pnpm i vite-plugin-vue-setup-extend -D
```

2. 配置 vite.config.ts

```js
import VueSetupExtend from 'vite-plugin-vue-setup-extend'

export default defineConfig ({
    plugins: [
        VueSetupExtend()
    ]
})
```

3. 使用

```html
<script lang="ts" setup name="xxx">
// ...
</script> 
```

**注意**

在使用 vite-plugin-vue-setup-extend 0.4.0 及以前版本时，会有个问题：如果 script 标签内没有内容，即使给 script 标签添加上 name 属性，其在 vue-devtools 内也不会生效。

解决办法: 不要让script标签内空着，例如：加行注释。

```html
<script lang="ts" setup name="xxx">
// test
</script> 
```
