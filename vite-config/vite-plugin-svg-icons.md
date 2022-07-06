# 雪碧图优化

在实际的项目中我们还会经常用到各种各样的 svg 图标，虽然 svg 文件一般体积不大，但 Vite 中对于 svg 文件会始终打包成单文件，大量的图标引入之后会导致网络请求增加，大量的 HTTP 请求会导致网络解析耗时变长，页面加载性能直接受到影响。

```shell
pnpm i vite-plugin-svg-icons -D
```

配置 vite.config.ts

```js
import { createSvgIconsPlugin } from 'vite-plugin-svg-icons';

{
  plugins: [
    // 省略其它插件
    createSvgIconsPlugin({
      iconDirs: [path.join(__dirname, 'src/assets/icons')]
    })
  ]
}
```

在 src/components目录下新建SvgIcon组件:

```html

<template>
    <svg aria-hidden="true" class="svg-icon" :style="{ fontSize: `${size}px`, color }">
        <use :xlink:href="symbolId" />
    </svg>
</template>

<script lang="ts" setup>
import { computed } from 'vue';

const props = defineProps({
    prefix: {
        type: String,
        default: 'icon'
    },
    name: {
        type: String,
        required: true
    },
    color: {
        type: String,
        default: '#333'
    },
    size: {
        type: [Number, String],
        default: 26
    }
});

const symbolId = computed(() => `#${props.prefix}-${props.name}`);
</script>

<style lang="scss" scoped>
.svg-icon {
    width: 1em;
    height: 1em;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
}
</style>
```

在src/main.tsx文件中添加一行代码:

```js
import 'virtual:svg-icons-register';
```

