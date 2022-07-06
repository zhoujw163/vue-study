# scss 配置

```shell
pnpm i sass -D
```

配置 vite.config.ts，让scss 变量，函数全局使用

```js
export default defineConfig({
    css: {
        preprocessorOptions: {
            scss: {
                // additionalData 的内容会在每个 scss 文件的开头自动注入
                additionalData: `@import "@/styles/settings/variable.scss";@import "@/styles/tool/index.scss";`
            }
        }
    },
})

```