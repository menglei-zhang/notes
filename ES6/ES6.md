### Chrome 和 Firefox 浏览器对 ES6 新特性最友好，IE7~11 基本不支持 ES6。

## Node.js 是运行在服务端的 JavaScript，它对 ES6 的支持度更高。



### Generator 函数

## ES6 新引入了 Generator 函数，可以通过 yield 关键字，把函数的执行流挂起，为改变执行流程提供了可能，从而为异步编程提供解决方案。

## Generator 函数组成
Generator 有两个区分于普通函数的部分：
一是在 function 后面，函数名之前有个 * ；
函数内部有 yield 表达式。
其中 * 用来表示函数为 Generator 函数，yield 用来定义函数内部的状态。

## 执行机制
调用 Generator 函数和调用普通函数一样，在函数名后面加上()即可，
但是 Generator 函数不会像普通函数一样立即执行，而是返回一个指向内部状态对象的指针，
所以要调用遍历器对象Iterator 的 next 方法，指针就会从函数头部或者上一次停下来的地方开始执行。







### ES6 函数














### ES6中的 Promise 的本质是要解决 地狱回调 的问题，并不能介绍代码量

## Promise 是一个 构造函数  可以通过 new Promise()  得到一个 Promise 实例

## 在Promise 上，有两个函数，分别是 resolve（成功之后的回调） 和 reject（失败之后的回调）

## 在 Promise 狗仔函数的 Prototype 属性上，有一个 .then() 方法，只要是Promise构造函数创建的实例，都可以访问到 .then() 方法

## Promise 表示一个异步操作，当new一个Promise的实例，这个实例就表示一个具体的异步操作

## 既然Promise创建爱你的实例是一个异步操作，那么，这个异步操作的结果只能有两种状态
# 状态1：异步执行成功了，需要在内部调用成功的回调函数resolve 把结果返回给调用者；
# 状态2：异步执行失败了，需要在内部调用失败的回调函数reject 把结果返回给调用者；
# 由于Promise的实例，是以个异步操作，所以内部拿到操作的结果后，无法使用return 把操作的结果返回给调用者；这时候，只能使用回调函数的形式 来把 成功 或者 失败 的结果 返回给调用者；

## 我们可以在new出来的Promise实例上，调用.then() 方法，【预先】 为这个Promise异步操作指定成功（resolve）和 失败（reject)回调函数

function getFileByName(fpath) {
    var promise = new Promise(function (resolve, reject) {
        fs.readFile(fpath, 'utf-8', (err, data) => {
            if (err) return reject(err)
            resolve(data)
        })
    })
    return promise
}
var p = getFileByName(path.join(__dirname, './file/1.txt'))

// console.log(p);   // Promise { <pending> }

// p.then(function(data){
//     console.log(data);
// }, function(err){
//     console.log(err.message);
// })

p.then(function(data){
    console.log(data);
}).catch(function(err){
    console.log(err.message);
})

无法取消 Promise ，一旦新建它就会立即执行，无法中途取消。

如果不设置回调函数，Promise 内部抛出的错误，不会反应到外部。

当处于 pending 状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。


### async

async 是 ES7 才有的与异步操作有关的关键字，和 Promise ， Generator 有很大关联的。







#### 16、Promise

## Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。
## 简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。
## 从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。
## Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

### Promise对象有以下两个特点。
## （1）对象的状态不受外界影响。
Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）。
只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。
## （2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。
Promise对象的状态改变，只有两种可能：从pending变为fulfilled和从pending变为rejected。
只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。
如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。
此外，Promise对象提供统一的接口，使得控制异步操作更加容易

## Promise也有一些缺点。
首先，无法取消Promise，一旦新建它就会立即执行，无法中途取消。
其次，如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。
第三，当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

### ES6 规定，Promise对象是一个构造函数，用来生成Promise实例。

const promise = new Promise(function(resolve, reject) {
    if( ) {
        resolve(value);
    }else {
        reject(error);
    }
})

promise.then(function(){

},function(error){
    
})