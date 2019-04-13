## 问题描述：利用async/await实现一个红绿灯效果   绿灯3s,红灯2s,黄灯1s
- async后面跟一个普通函数会返回一个promise
- await只能在async函数内部使用,用来等待一个异步函数执行完毕，将异步以同步形式

```
async function test(){
  return 'test'
}
test().then((val) => {
  console.log(val) //打印test
})

//定义一个睡眠函数  time时间后执行
function sleep(time){
  return new Promise((resolve, reject) => {
    setTimeout(resolve, time)
  })
}

async tmp(){
  await sleep(3000);//等待3s
}
```

#### 模拟红绿灯
```
//该函数用于完成等待
function sleep(time){
  return new Promise((resolve, reject) => {
    setTimeout(resolve, time)
  })
}
async function changeColor(color, duration){
  dom.style.backgroundColor = color;
  await sleep(duration)
}

async function execute(){
  await changeColor('green', 3000);
  await changeColor('red', 2000);
  await changeColor('yellow', 1000);
}
```
