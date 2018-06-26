**审读NodeJs获取的收获**

1. Reflect对象的用法
 - 定义对象属性以及值—Reflect.defineProperty(obj, attr, value:{ value: ?,  writable: false, enumerable: false, configurable: false })与Object.defineProperty(obj, attr, value:{ value: ?,  writable: false, enumerable: false, configurable: false })
 - 调用函数—Reflect.apply(func, obj, args)与Function.apply(obj, args)
 - 构建对象—Reflect.construct(obj, args)与new obj()
 - 删除对象属性—Reflect.deleteProperty(obj, attr)与delete obj.attr
 - 获取对象属性值—Reflect.get(obj, attr, receiver)与obj.attr
 - 设置对象属性值—Reflect.set(obj, attr, value, receiver)与obj.attr = xxx
 - 获取对象的属性描述—Reflect.getOwnPropertyDescritptor(obj, attr)与Object.getOwnPropertyDescriptor(obj, attr)
 - 获取对象的原型—Reflect.getPrototypeOf(obj)与Object.getPrototypeOf(obj)
 - 检测对象的属性—Reflect.has(obj, attr)与attr in obj
 - 检察元素是否可以扩展—Reflect.isExtensible(obj),Reflect.preventExtensions阻止对象扩展
 - 获取对象的所有键—Reflect.ownKeys(obj)
 - 设置对象的原型—Reflect.setPrototypeOf(obj, prototype)与Object.setPrototypeOf(obj, prototype) 
2. js中的getter与setter

 ```
    var obj = { 
     get sex() { return this._sex }, 
     set sex(val) { this._sex = val }
    };
    或者 
    var obj = Object.create(null,
    { 
      sex: { 
        get: function() { return this._sex; }, 
        set: function(val) { this._sex = val; } 
        } 
    };);
    
    obj.sex = 'man'; // 自动调用set方法设置sex的值
    
    console.log(obj.sex);  // 自动调用get方法获取sex值
 ```
3. obj上的方法
 - 对象是否含有当前属性—obj.hasOwnProperty, obj.prototype.hasOwnProperty
 - 是否是某对象的原型—obj.isPrototypeOf, obj.prototype.isPrototypeOf
 
4. Object上的方法
- 创建一个具有指定原型且可选择性地包含指定属性的对象—Object.create(prototype, attr: { attr: { value: ?, writable: false, enumerable: false, configurable: false }, ... })
- 要返回其枚举自身属性的对象—Object.keys(obj)

5. obj属性相关
- configurable: true, // 是否可删除，delete操作符是否可用， 默认false
- enumerable: true, // 是否可枚举， for-in循环， 默认true
- writable: false // 是否可修改， 默认true

6. Proxy对象，处理器对象用来自定义代理对象的各种可代理操作。可代理方法包括：
- handler.apply() —用于拦截函数的调用。
- handler.construct() —用于拦截new 操作符. 为了使new操作符在生成的Proxy对象上生效，用于初始化代理的目标对象自身必须具有[[Construct]]内部方法（即 new target 必须是有效的）。
- handler.defineProperty() —拦截对对象的 Object.defineProperty() 操作。
- handler.deleteProperty() —用于拦截对对象属性的 delete 操作。
- handler.get() —用于拦截对象的读取属性操作。
- handler.getOwnPropertyDescriptor() —方法是 Object.getOwnPropertyDescriptor()  的陷阱。
- handler.getPrototypeOf() —是一个代理方法，当读取代理对象的原型时，该方法就会被调用。
- handler.has() —方法可以看作是针对 in 操作的钩子.
- handler.isExtensible() —用于拦截对对象的Object.isExtensible()。
- handler.ownKeys() —方法用于拦截 Reflect.ownKeys().
- handler.preventExtensions() —用于拦截Object.preventExtensions().
- handler.set() —用于拦截设置属性值的操作。
- handler.setPrototypeOf() —用来拦截 Object.setPrototypeOf().

7. Symbol类型，一种新的原始数据类型Symbol，表示独一无二的值。
- Symbol函数可以接受一个字符串作为参数，表示对Symbol实例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分。var s1 = Symbol();var s2 = Symbol('test');
- 作为属性名的Symbol

```
   var mySymbol = Symbol();
   // 第一种写法
   var a = {};
   a[mySymbol] = 'Hello!';
   // 第二种写法
   var a = {
     [mySymbol]: 'Hello!'
   };
   // 第三种写法
   var a = {};
   Object.defineProperty(a, mySymbol, { value: 'Hello!' });
   // 以上写法都得到同样结果
   a[mySymbol] // "Hello!"
```
- Symbol.for()，Symbol.keyFor()

    Symbol.for机制有点类似于单例模式，首先在全局中搜索有没有以该参数作为名称的Symbol值，如果有，就返回这个Symbol值，否则就新建并返回一个以该字符串为名称的Symbol值。和直接的Symbol就点不同了。
    
    Symbol.keyFor方法返回一个已登记的Symbol类型值的key。实质就是检测该Symbol是否已创建
```
    var s1 = Symbol.for('foo');
    var s2 = Symbol.for('foo');
    
    s1 === s2 // true
    
    var s1 = Symbol.for("foo");
    Symbol.keyFor(s1) // "foo"
    
    var s2 = Symbol("foo");
    Symbol.keyFor(s2) // undefined

```
8. Map对象的使用
- Map.prototype.size
- Map.prototype.clear()
- Map.prototype.delete(key)
- Map.prototype.entries()
- Map.prototype.forEach(callbackFn[, thisArg])
- Map.prototype.get(key)
- Map.prototype.has(key)
- Map.prototype.keys()
- Map.prototype.set(key, value)
- Map.prototype.values()
```
    // Map的定义以及设置、取值
    var myMap = new Map();
    
    var keyString = 'a string',
        keyObj = {},
        keyFunc = function() {};
    
    // setting the values
    myMap.set(keyString, "value associated with 'a string'");
    myMap.set(keyObj, 'value associated with keyObj');
    myMap.set(keyFunc, 'value associated with keyFunc');
    
    myMap.size; // 3
    
    // getting the values
    myMap.get(keyString);    // "value associated with 'a string'"
    myMap.get(keyObj);       // "value associated with keyObj"
    myMap.get(keyFunc);      // "value associated with keyFunc"
    
    myMap.get('a string');   // "value associated with 'a string'"
                             // because keyString === 'a string'
    myMap.get({});           // undefined, because keyObj !== {}
    myMap.get(function() {}) // undefined, because keyFunc !== function () {}
```
```
    // Map的遍历方法for...of以及forEach
    var myMap = new Map();
    myMap.set(0, 'zero');
    myMap.set(1, 'one');
    for (var [key, value] of myMap) {
      console.log(key + ' = ' + value);
    }
    // 0 = zero
    // 1 = one
    
    for (var key of myMap.keys()) {
      console.log(key);
    }
    // 0
    // 1
    
    for (var value of myMap.values()) {
      console.log(value);
    }
    // zero
    // one
    
    for (var [key, value] of myMap.entries()) {
      console.log(key + ' = ' + value);
    }
    // 0 = zero
    // 1 = one
    
    myMap.forEach(function(value, key) {
      console.log(key + ' = ' + value);
    });
    // Will show 2 logs; first with "0 = zero" and second with "1 = one"
```
```
    // Map的初始化
    var first = new Map([
      [1, 'one'],
      [2, 'two'],
      [3, 'three'],
    ]);
    
    var second = new Map([
      [1, 'uno'],
      [2, 'dos']
    ]);
    
    // Merge two maps. The last repeated key wins.
    // Spread operator essentially converts a Map to an Array
    var merged = new Map([...first, ...second]);
    
    console.log(merged.get(1)); // uno
    console.log(merged.get(2)); // dos
    console.log(merged.get(3)); // three
```
9. Assert，断言
- assert(value[,message])/assert(value[,message])
    assert()是assert.ok()的简写方式，两者用法一样。
    如果value的值为true，那么什么也不会发生。如果value为false，将抛出一个信息为message的错误。
10. Function.length
- length是函数对象的一个属性值，指该函数有多少个必须要传入的参数，即形参的个数。形参的数量不包括剩余参数个数，仅包括第一个具有默认值之前的参数个数。与之对比的是，  arguments.length 是函数被调用时实际传参的个数。