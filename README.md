# 2020-前端面试集锦
2020年 ，即将到来，金三银四面试黄金季,一定要抓住。本博客总结常见的面试题，查漏补缺,希望对你有所帮助。
# 技巧
- 遇到比较抽象的问题就具体化(举例子)，遇到比较具体的题目就抽象化(阐述)。
- 抽象题目搜知乎，代码题目搜Stackoverflow 或者博客。
- 『XXX 的原理』这种题目一般来说都是说一下源代码的思路，但不需要看源代码，直接看别人总结好的博客即可。(尽量不要使用百度)

# HTML 
- 你是如何理解HTML 语义化的？
 **参考答案**：
       1.举例法 
  HTML  语义化就是使用正确的标签（总结）。段落就写 p 标签，标题就写h1标签， 
 文章就写article标签，视频就写video标签，等等。
            2.阐述法
首先将以前后台开发人员使用  table布局，然后将美工人员使用div+css布局，最后讲专业的前端会使用正确的标签进行页面开发。

 - meta viemport 是 做什么的，怎么写？ 
   **参考答案**：
举例法 ： 
`<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1">`
然后逐个解释每个单词的意思即可。

- 你平时用过哪些HTML5标签？
你平时用的html5标签列举出来即可，要注意如果这个标签的用法比较复杂，你要先看一下MDN的文档 ，如果你说出的标签，却不知道它有哪些API，那就会比较麻烦。

 **参考答案**：最简单的演示
```
<header>
  <nav></nav>
</header>
<main>
  <section></section>
</main>
<footer></footer>
```
- H5 是什么？
[参考这里](https://www.zhihu.com/question/30363342)


# CSS 
- 两种盒模型 说一下？？
 **参考答案**：
IE盒模型border-box和W3C盒模型content-box。区别在于IE的content部分把 border 和 padding计算了进去。box-sizing:border-box; border-box更好用，我平时更喜欢。
- 如何垂直居中？？
 **参考答案**：
如果父元素height不定，直接子元素padding:10px 0;就垂直居中了
如果父元素给定height：
·table标签自带。
·子元素用两个span包起来，子元素和span display:inline-block,vertical-align: middle;，
span height:100%。
·子元素position:absolute;top: 50%;margin-top: -50px;或者用translate(-50%,-50%);
·子元素position:absolute;left:0;top:0;margin: auto;
·父元素display: flex; justify-content: center;align-items: center;
- flex怎么用？常用的属性有哪些？？
 **参考答案**：
·flex-direction: row左起 | row-reverse右起 | column上起 | column-reverse下起;
·flex:无单位值（flex-grow），无单位值（flex-shrink），有效宽度值（flex-basis）后两个
值可选 flex:auto（0,1,auto）,flex:none（0,0auto）,flex:initial（1,1auto）

- BFC 是什么？？
 **参考答案**： 
[BFC是什么(参考)](https://www.jianshu.com/p/e6a7cdbae7b7)
- CSS 选择器优先级
**简答**：
1.越具体的优先级就越高
2.同样优先级写在后面的会覆盖前面的
3.!important 优先级最高，(谨慎使用)

- 清除浮动说一下  背代码
```
clearfix:after{
  content: '';
display: block; /* 或者table*/
clear: both;
}

.clearfix{
     zoom: 1; /* IE 兼容*/
 }
```
#原生JS

- ES6语法知道那些，分别怎么用？
 **参考答案**： 
举例法
 let const 箭头函数 promise 展开操作符 默认参数 import export 等，具体的请参考这里[ES 6 新特性列表](https://fangyinghang.com/es-6-tutorials/)

- Promise Promise.all Promise.rase 分别怎么用 
 **参考答案**： 
先理解一下 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对Promise的描述。Promise 对象是一个代理对象（代理一个值），被代理的值在Promise对象创建时可能是未知的。它允许你为异步操作的成功和失败分别绑定相应的处理方法（handlers）。 这让异步方法可以像同步方法那样返回值，但并不是立即返回最终执行结果，而是一个能代表未来出现的结果的promise对象.
```
function fn() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      // 返回一个随机数 1-6
      let n = parseInt(Math.random() * 6 + 1, 10);
      resolve(n);
    }, 3000);
  });
}
// 如果成功了 resolve(n) 的结果 会  传给 .then()的第一个参数 x
fn().then(
  x => {
    console.log("筛子的点数是" + x);
  },
  () => {
    console.log("摇色子不会失败");
  }
);
```
背代码 Promise.all 用法 
```Promise.all([promise1, promise2]).then(success1, fail1)```
promise1和promise2都成功才会调用success1

背代码 Promise.race 用法
``` Promise.race([promise1, promise2]).then(success1, fail1)```
promise1和promise2只要有一个成功就会调用success1

- 手写函数防抖 和函数节流 
 **参考答案**： [函数节流与防抖](https://www.jianshu.com/p/1b7c5d0ef0e4)

背代码
 // 节流（一段时间执行一次之后，就不执行第二次）
```
 function throttle(fn, delay){
     let canUse = true
     return function(){
         if(canUse){
             fn.apply(this, arguments)
             canUse = false
             setTimeout(()=>canUse = true, delay)
         }
     }
 }

 const throttled = throttle(()=>console.log('hi'))
 throttled()
 throttled()
```
注意，有些地方认为节流函数不是立刻执行的，而是在冷却时间末尾执行的（相当于施法有吟唱时间），那样说也是对的。

背代码
 // 防抖（一段时间会等，然后带着一起做了）
``` function debounce(fn, delay){
     let timerId = null
     return function(){
         const context = this
         if(timerId){window.clearTimeout(timerId)}
         timerId = setTimeout(()=>{
             fn.apply(context, arguments)
             timerId = null
         },delay)
     }
 }
 const debounced = debounce(()=>console.log('hi'))
 debounced()
 debounced()
```
- 手写AJAX
 **参考答案**：
背代码，完整版
```
 var request = new XMLHttpRequest()
 request.open('GET', '/a/b/c?name=ff', true);
 request.onreadystatechange = function () {
   if(request.readyState === 4 && request.status === 200) {
     console.log(request.responseText);
   }};
 request.send();
```
背代码，简化版

```
 var request = new XMLHttpRequest()
 request.open('GET', '/a/b/c?name=ff', true)
 request.onload = ()=> console.log(request.responseText)
 request.send()
```


- 这段代码里的 this 是什么？
 **参考答案**：
```
1.fn()  // this => window/global
2.obj.fn() // this => obj
3.fn.call(xxx) // this => xxx 
4.fn.apply(xxx) // this => xxx
5.fn.bind(xxx) // this => xxx
6.new fn() // this => 这个新的对象 
7.fn = ()=>{} // this => 外面的this  
```
看调用 参考 方方的文章  [this 的值到底是什么？一次说清楚](https://zhuanlan.zhihu.com/p/23804247)

- 闭包/立即执行函数是什么？ 
 **参考答案**：
直接看文章
 [闭包 ](https://zhuanlan.zhihu.com/p/22486908)
 [什么是立即执行函数？有什么作用？](https://zhuanlan.zhihu.com/p/22465092)

- 什么是 JSONP，什么是 CORS，什么是跨域？
 **参考答案**： 
[跨域的几种实现方式与原理](https://www.jianshu.com/p/a0b066c0c976)

- async/await怎么用？如何捕获异常
**参考答案**：
[await 和 async 的用法](https://www.jianshu.com/p/63a5ca0fe51d)

- 如何实现深拷贝？ 
 **参考答案**：  要点 
1. 递归
2.判断类型 
3.检查环(循环引用)
4.需要忽略原型
- 如何用正则实现trim() (去除字符串左右两端的空格)
 **参考答案**：
```
String.prototype.trim = function(){
    return this.replace(/^\s+|\s+$/g, '')
}
//或者 
function trim(string){
    return string.replace(/^\s+|\s+$/g, '')
}
```
- 不用class 如何实现继承 ？ 用class又如何实现
 **参考答案**： 背代码
不用 class 这样实现
```
 function Animal(color){
     this.color = color
 }
 Animal.prototype.move = function(){} // 动物可以动
 function Dog(color, name){
     Animal.call(this, color) // 或者 Animal.apply(this, arguments)
     this.name = name
 }
 // 下面三行实现 Dog.prototype.__proto__ = Animal.prototype
 function temp(){}
 temp.prototye = Animal.prototype
 Dog.prototype = new temp()

 Dog.prototype.constuctor = Dog // 这行看不懂就算了，面试官也不问
 Dog.prototype.say = function(){ console.log('汪')}

 var dog = new Dog('黄色','阿黄')
```
用class  实现
```
class Animal{
     constructor(color){
         this.color = color
     }
     move(){}
 }
 class Dog extends Animal{
     constructor(color, name){
         super(color)
         this.name = name
     }
     say(){}
 }
```
- 如何实现数组去重？
 **参考答案**：
1 .计数排序变形，背代码
2.使用 Set（面试已经禁止这种了，因为太简单）
3.使用 Weak Map
-  == 相关题目  (没有规律 ) 建议反着答即可 
- 手写一个 Promise （极难） 抽空有时间 建议 学会 
参考 [https://juejin.im/post/5aafe3edf265da238f125c0a](https://juejin.im/post/5aafe3edf265da238f125c0a "null")

#DOM 
- 事件委托 
**参考答案** :
简易版 （有缺陷 没有考虑子元素 ）: bug 在于，如果用户点击的是 li 里面的 span，就没法触发 fn，这显然不对
```
  ul.addEventListener('click',function(e){
  if(e.target.tagName.toLowerCase() === 'li'){
    fn() // 执行某个函数 
    //console.log('您点击了li')
  }
})
。
```
高级版 ：思路是点击 span 后，递归遍历 span 的祖先元素看其中有没有 ul 里面的 li。
```
function delegate(element, eventType, selector, fn) {
     element.addEventListener(eventType, e => {
       let el = e.target
       while (!el.matches(selector)) {
         if (element === el) {
           el = null
           break
         }
         el = el.parentNode
       }
       el && fn.call(el, e, el)
     })
     return element
   }
```
- 用mouse事件 写一个可以拖拽的div
**参考答案** : 该题考察的比较全面  [http://js.jirengu.com/mowevogufa/8/edit](http://js.jirengu.com/mowevogufa/8/edit)


```
//HTML 部分 
<div id="xxx"></div>
// CSS部分 
div{
  border: 1px solid red;
  position: absolute;
  top: 0;
  left: 0;
  width: 100px;
  height: 100px;
}
*{margin:0; padding: 0;}
//JS部分 
var dragging = false 
var position = null 
xxx.addEventListener("mousedown",function(e){
  dragging = true 
  position = [e.clientX,e.clientY]
})

document.addEventListener('mousemove',function(e){
  if(dragging === false){return}
  console.log('hi')
  const x = e.clientX
  const y = e.clientY
  const deltaX = x-position[0]
  const deltaY = y-position[1]
  const left = parseInt(xxx.style.left || 0)
  const  top = parseInt(xxx.style.top || 0)
  xxx.style.left = left + deltaX + 'px'
  xxx.style.top = top+deltaY +'px'
  position= [x,y]
})
document.addEventListener("mouseup",function(e){
  console.log("停止")
  dragging = false
})
```
#HTTP
- HTTP 状态码知道哪些？分别什么意思？ 
 **参考答案** ：
— 2xx 表示成功
— 3xx 表示需要进一步操作 
— 4xx 表示浏览器（客户端）方面出错 
— 5xx 表示服务器方面出错 
— 完整参考  [http://www.runoob.com/http/http-status-codes.html](http://www.runoob.com/http/http-status-codes.html "null")
- HTTP 缓存有哪几种？ 
**参考答案**：*   需要详细的了解 ETag、CacheControl、Expires 的异同
--  参考 [https://imweb.io/topic/5795dcb6fb312541492eda8c](https://imweb.io/topic/5795dcb6fb312541492eda8c "null")
答题要点 
1.ETag 是通过对比浏览器和服务器资源的特征值（如MD5）来决定是否要发送文件内容，如果一样就只发送 304（not modified）
2.Expires 是设置过期时间（绝对时间），但是如果用户的本地时间错乱了，可能会有问题
3.CacheControl: max-age=3600 是设置过期时长（相对时间），跟本地时间无关。

- GET 和 POST 的区别 （常考）
**参考答案**：（误解颇多 错解，但是能过面试）
1.GET在浏览器回退时是无害的，而POST会再次提交请求。
2.GET产生的URL地址可以被加入收藏栏，而POST不可以。
3.GET请求会被浏览器主动cache，而POST不会，除非手动设置。
4.GET请求只能进行url编码，而POST支持多种编码方式。
5.GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
6.GET请求在URL中传送的参数是有长度限制的，而POST么有。
7.对参数的数据类型，GET只接受ASCII字符，而POST没有限制。
8.GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。
9.GET参数通过URL传递，POST放在Request body中

正解：就一个区别：语义——GET 用于获取资源，POST 用于提交资源
详细请参考 ： [https://zhuanlan.zhihu.com/p/22536382](https://zhuanlan.zhihu.com/p/22536382 "null")

- Cookie V.S. LocalStorage V.S. SessionStorage V.S. Session
**参考答案**：
1、Cookie V.S. LocalStorage
       主要区别是 Cookie 会被发送到服务器，而 LocalStorage 不会
      Cookie 一般最大 4k，LocalStorage 可以用 5Mb 甚至 10Mb（各浏览器不同）
2、LocalStorage V.S. SessionStorage
LocalStorage 一般不会自动过期（除非用户手动清除），而 SessionStorage 在回话结束时过期（如关闭浏览器）
3、Cookie V.S. Session
Cookie 存在浏览器的文件里，Session 存在服务器的文件里
Session 是基于 Cookie 实现的，具体做法就是把 SessionID 存在 Cookie 里
 