# Set & Map

## Sets

### 使用Set实现数组去重

在ES6中，因为Set只存储唯一值，所以你可以使用Set删除重复项。

```js
let arr = [1, 1, 2, 2, 2, 3, 3];
let deduped = [...new Set(arr)]; // [1,2,3]
```

### 对Set使用数组方法

使用扩展运算符就可以简单的将Set转换为数组。所以你可以对Set使用Array的所有原生方法。

比如我们想要对下面的Set进行filter操作，获取大于3的项。

```js
let mySet = new Set([1, 2, 3, 4, 5]);
let filtered = [...mySet].filter(x => x > 3)
filtered; // [4, 5]
```