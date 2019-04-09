### 模拟实现call方法
原理：
1. 将函数赋值给对象
2. 执行函数
3. 返回值
```
Function.prototype.myCall = function(context){
  context = context || window;
  context.fn = this;
  var args = [...arguments].slice(1);
  var result = context.fn(...args);
  delete context.fn;
  return result;
}
```
***
### 模拟实现apply方法
```
Function.prototype.myApply = function(context){
  context = context || window;
  context.fn = this;
  var result;
  if(arguments[1]){
    result = context.fn(...arguments[1]);
  }else{
    result = context.fn();
  }
  delete context.fn;
  return result;
}
```
***
### 模拟实现bind方法
##### bind方法与call,apply区别是会返回一个新的函数
```
Function.prototype.myBind = function(context){
  var _this = this;
  var args = [...arguments].slice(1);
  return function F(){
    if(this instanceof F){
      return new _this(...args, ...arguments)
    }
    return _this.apply(context, args.concat(...arguments))
  }
}
```
