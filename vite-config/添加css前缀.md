# css 添加前缀

```shell
pnpm i autoprefixer -D
```

``` js
// postcss.config.js
module.exports = {
    plugins: [
        require('autoprefixer')({
            // 指定目标浏览器
            overrideBrowserslist: ['> 0.5%, not dead, not ie']
        })
    ]
};
```