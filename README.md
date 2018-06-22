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

     `
     var obj = { get sex() { return this._sex }, set sex(val) { this._sex = val } };
     或者 var obj = Object.create(null, { sex: { get: function() { return this._sex; }, set: function(val) { this._sex = val; } } };);
     `
     
     ` obj.sex = 'man'; // 自动调用set方法设置sex的值`
     
     `console.log(obj.sex);  // 自动调用get方法获取sex值`
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