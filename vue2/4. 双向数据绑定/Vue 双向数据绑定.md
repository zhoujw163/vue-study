# Vue 双向数据绑定

涉及到的技术

-   Object.defineProperty
-   Observer
-   Watcher
-   Dep
-   Directive

分为三步理解

1. [数据监听](./1.%20数据监听.md)
2. [依赖收集](2.%20依赖收集.md)
3. [派发更新](3.%20派发更新.md)

## 认识 Object.defineProperty

```js
function defineReactive(data, key, value) {
    Object.defineProperty(data, key, {
        configurable: true,
        enumerable: true,
        get: function () {
            console.log(`get ${value}`);
            return value;
        },
        set: function (newVal) {
            console.log(`set key: ${key} value ${newVal}`);
            value = newVal;
        }
    });
}

function observer(data) {
    Object.keys(data).forEach(key => {
        defineReactive(data, key, data[key]);
    });
}

let obj = { a: 1 };
let arr = [1, 2, 3];

observer(obj);
observer(arr);

arr.unshift(4);
// get 3
// get 2
// set key: 2 value 2
// get 1
// set key: 1 value 1
// set key: 0 value 4
```

object.defineProperty 可以对对象某个 key 值进行重写，只能重写已有的值，对于新增的 key 值无法重写。

执行 arr.unshift(4) 为什么频繁的触发 get 和 set？

因为数组在内存中的存储是连续的，存储的是数组的起始位置和长度。执行 arr.unshift(4)，会先增加数组长度，取出原先最后一位放到现在的最后一位。原先只对下标为 0，1，2 重写了 get，set 没有对新增的下标 3 重写，因此只会触发下标为 2 的 get，不触发下标为 3 的 set。同理一次对下标 0，1 做同样的操作。最后将要 4，填到下标为 0 的位置，即触发 0 的 set。

![observer](../../images/observer.png)
