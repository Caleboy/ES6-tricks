# Symbol

ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值，可以保证不会与其他属性名产生冲突。

它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

为了说明 Symbol 的作用，我们来描述一个使用场景。

## 消除魔术字符串

魔术字符串指的是，在代码之中多次出现、与代码形成强耦合的某一个具体的字符串或者数值。风格良好的代码，应该尽量消除魔术字符串，改由含义清晰的变量代替。

```js
function getArea(shape, options) {
  let area = 0;

  switch (shape) {
    case 'Triangle': // 魔术字符串
      area = .5 * options.width * options.height;
      break;
    /* ... more code ... */
  }

  return area;
}

getArea('Triangle', { width: 100, height: 100 }); // 魔术字符串
```

上面代码中，字符串Triangle就是一个魔术字符串。它多次出现，与代码形成“强耦合”，不利于将来的修改和维护。

常用的消除魔术字符串的方法，就是把它写成一个变量。

```js
const shapeType = {
  triangle: 'Triangle'
};

function getArea(shape, options) {
  let area = 0;
  switch (shape) {
    case shapeType.triangle:
      area = .5 * options.width * options.height;
      break;
  }
  return area;
}

getArea(shapeType.triangle, { width: 100, height: 100 });
```

上面代码中，我们把Triangle写成shapeType对象的triangle属性，这样就消除了强耦合。

如果仔细分析，可以发现shapeType.triangle等于哪个值并不重要，只要确保不会跟其他shapeType属性的值冲突即可。因此，这里就很适合改用 Symbol 值。

```js
const shapeType = {
  triangle: Symbol()
};
```

上面代码中，除了将shapeType.triangle的值设为一个 Symbol，其他地方都不用修改。

下面是另外一个例子。

## redux

```js
const REQUEST_STARTED = Symbol();
const REQUEST_COMPELTED = Symbol();
const REQUEST_FAILED = Symbol();
const request = createAction(REQUEST_STARTED);
const success = createAction(REQUEST_COMPELTED, null, (...args) => args[1]);
const failure = createAction(REQUEST_FAILED);

function reducer(state, action) {
  switch (action.type) {
    case REQUEST_STARTED:
      return SREQUEST_STARTEDstate;
    case REQUEST_COMPELTED:
      return REQUEST_COMPELTEDstate;
    case REQUEST_FAILED:
      return REQUEST_FAILEDstate;
    default:
      throw state;
    }
}
```

常量使用 Symbol 值最大的好处，就是其他任何值都不可能有相同的值了，因此可以保证上面的switch语句会按设计的方式工作。