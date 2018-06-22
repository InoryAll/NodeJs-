**审读NodeJs获取的收获**

1. Reflect对象的用法
 - 定义对象属性以及值—Reflect.defineProperty(obj, attr, value:{ value: ?,  writable: false, enumerable: false, configurable: false })与Object.defineProperty(obj, attr, value:{ value: ?,  writable: false, enumerable: false, configurable: false })
 - 调用函数—Reflect.apply(func, obj, args)与Function.apply(obj, args)
 - 构建对象—Reflect.construct(obj, args)与new obj()
 - 删除对象属性—Reflect.deleteProperty(obj, attr)与delete obj.attr
 - 获取对象属性值—Reflect.get(obj, attr)与obj.attr
 - 设置对象属性值—Reflect.set(obj, attr, value)与obj.attr = xxx
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