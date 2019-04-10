# 深浅拷贝
## 浅拷贝
浅拷贝即只拷贝对象第一层,可通过以下方式实现
1. var target = Object.assign({}, origin)
2. var target = {...origin}  ES6展开运算符

## 深拷贝
即深层次的拷贝，递归拷贝对象的属性
1. var target = JSON.parse(JSON.stringify(origin))<br/>
缺点: 
      - 无法序列化函数
      - 会忽略undefined,Symbol值
      - 无法处理递归调用
      - 忽略RegExp,Date直接转成字符串形式
2. 递归实现拷贝
```
function deepClone(obj){
  if(obj instanceof Date) return new Date(obj)
  if(obj instanceof RegExp) return new RegExp(obj)
  if(obj === null || typeof obj != 'function') return obj;
  //获取构造函数 []或者{}
  var tmp = new obj.constructor();
  for(var key in obj){
    tmp[key] = deepClone(obj[key])
  }
  return tmp;
}
```
3. 使用lodash的深拷贝方法,考虑的比较全面
