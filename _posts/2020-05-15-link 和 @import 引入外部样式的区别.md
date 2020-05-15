## link 和 @import 引入外部样式的区别
```shell
	在使用外链的方式去引入css的时候，有2种方式 link 和 @import
	区别在于：
		1.link引入的时候就会去加载css
		  但是@import是在页面加载完毕的时候才会被加载，
		  css的加载时候不会阻塞页面的解析但是其会阻塞页面渲染的，
		  所以使用import的时候，比较容易出现'闪屏'的现象
		2.其次import是css的语法 其只能写在css中，所以style标签或css文件中，
		是不可以和link一样直接被写在html文件中的
		3.link标签是html的标签，所以其即使用`rel='stylesheet'`来加载样式文件，
		也可以使用`rel = 'shortcut icon'`的方式来加载网页的缩略图
		而import是css的语法，所以只能加载css样式
		4.我们可以通过js操作dom的方式来操作页面的link元素，
		 但是没有办法来操作import方式加载的css
```
```js
<link rel="stylesheet" href="/css/style.css" id="css">
var cssLink = document.getElementById('css')
cssLink.href = '/css/another.css'
// 或使用下的方法
// var cssLink = document.getElementsByTagName('link')[0]
// cssLink.setAttribute('href', '/css/another.css')
```
```js
var link = document.createElement('link')
// link.setAttribute('type', 'text/css') // 可以不写
link.setAttribute('rel', 'stylesheet')
link.setAttribute('href', '/path/style.css')
document.body.appendChild(link) // 谁当父节点可以看具体需求
```
```css
/*  @import 的写法 */
@import 'style.css' //Windows IE4/ NS4, Mac OS X IE5, Macintosh IE4/IE5/NS4不识别
@import "style.css" //Windows IE4/ NS4, Macintosh IE4/NS4不识别
@import url(style.css) //Windows NS4, Macintosh NS4不识别
@import url('style.css') //Windows NS4, Mac OS X IE5, Macintosh IE4/IE5/NS4不识别
@import url("style.css") //Windows NS4, Macintosh NS4不识别
```
> 所以可以看出@import url(style.css) 和@import url("style.css")是最优的选择，兼容的浏览器最多。从字节优化（节省不必要的字符来降低文件大小）的角度来看@import url(style.css)最值得推荐。

![link和@import的执行过程](https://www.showdoc.cc/server/api/common/visitfile/sign/db764f20c7ea069483745cf6e02e71a4?showdoc=.jpg)
link和@import的执行过程

> link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载