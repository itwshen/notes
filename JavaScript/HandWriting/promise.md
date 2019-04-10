# Promise
## promise基本语法
1. promise有三种状态pending, fulfilled, rejected,
2. 状态只能从pending->fulfilled或 pending->rejected
3. promise构造函数立即执行,promise.then异步执行(微任务)

## 手写简易版promise
```
const PENDING = 'pending';
const RESOLVED = 'resolved';
const REJECTED = 'rejected';
function MyPromise(fn){
  var that = this;
  //作为then回调函数返回值
  that.value = null;
  that.state = PENDING;
  //存储成功失败回调
  that.resolvecallbacks = [];
  that.rejectcallbacks = [];
  
  //定义resolve,reject函数
  function resolve(value){
    if(that.state === PENDING){
      that.state = RESOLVED;
      that.value = value;
      //执行成功回调
      that.resolvecallbacks.forEach(cb => cb(that.value));
    }
  }
  function reject(e){
    if(that.state === PENDING){
      that.state = REJECTED;
      that.value = e;
      that.rejectcallbacks.forEach(cb => cb(that.value))
    }
  }
  //try...catch包裹捕获异常
  try{
    fn(resolve, reject);
  }catch(e){
    reject(e);
  }
}
//实现then函数
MyPromise.prototype.then = function(onFulFilled, onRejected){
  onFulFilled = typeof onFulFilled === 'function' ? onFulFilled : v => v;
  onRejected = typeof onRejected === 'function' ? onRejected : e => throw new Error(e)
  if(that.state === PENDING){
    that.resolvecallbacks.push(onFulFilled);
    that.rejectcallbacks.push(onRejected);
  }
  if(that.state === RESOLVED){
    onFulFilled(that.value)
  }
  if(that.state === REJECTED){
    onRejected(that.value)
  }
}
```
