### 总结（记录）一些`codeing`过程中用到的`tip`
#### <a href="#getKey">1. 获取json的`key`值</a>
#### <a href="#input">2. JS实时监听文本域的变化</a>
#### <a href="#checkType">3. JavaScript类型检验</a>
---
#### <a name="getKey">1. </a>获取json的 `key` 值
```javascript
var obj = { name: "naruto", age: 23, dad: "minato"}
````
##### 1.1. 使用 `for in` 来循环 :
```javascript
for (var key in obj){
    console.log(key) // 依次输出 "name", "age", "dad"
}
```
> 这种方法比较常见，相信大家看到这个问题时第一时间都会想到吧，但是我要介绍的是下面这个更简单的方法。
##### 1.2. 使用 `Object.keys()` 来获取 :
```
- console.log( Object.keys(obj) ) // 输出一个数组 ["name", "age", "dad"]
- 所以, 当我们需要某个key值时可以从当前数组中取得。
```
---
#### <a name="input">2. JS实时监听文本域的变化</a>
>  众所周知，使用 `onchange` 事件来监听文本域的变化是我们在开发中用到的最多的方法。但是， `onchange` 是在文本域失焦时才触发，有时候由于需求的原因，需要我们来实时监听文本域的变化，除了使用`keydown`和`keyup`外，我们还可以:
##### 2.1. 使用 `onpropertychange` 
```javascript
<input type="text" id="txt">

$("#ysy").bind('input propertychange', function() {  
    console.log(new Date().getTime()); 
});
```
##### 2.2 使用 `oninput` 
```javascript
document.getElementById('txt').oninput = function(){
    console.log(this.value);
}
```
> 最后，总结一下`onchange, onpropertychange`和`oninput`之间的异同：
1. `onchange`事件与`onpropertychange`事件的区别：`onchange`事件在内容改变（两次内容有可能还是相等的）且失去焦点时触发；`onpropertychange`事件却是实时触发，即每增加或删除一个字符就会触发，通过js改变也会触发该事件，但是该事件IE专有。
2. `oninput`事件与`onpropertychange`事件的区别：`oninput`事件是IE之外的大多数浏览器支持的事件，在value改变时触发，实时的，即每增加或删除一个字符就会触发，然而通过js改变value时，却不会触发；`onpropertychange`事件是任何属性改变都会触发的，而`oninput`却只在value改变时触发，`oninput`要通过`addEventListener()`来注册，`onpropertychange`注册方式跟一般事件一样。（此处都是指在js中动态绑定事件，以实现内容与行为分离）>
3. `oninput`与`onpropertychange`失效的情况：  （1）`oninput`事件：a). 当脚本中改变value时，不会触发；b).从浏览器的自动下拉提示中选取时，不会触发。  （2）`onpropertychange`事件：当input设置为`disable=true`后，onpropertychange不会触发。
---
#### <a name="checkType">3. JavaScript类型检验</a>
> 一个简单有用的js类型检验的方法
```javascript
function checkType(sth) {
    return Object.prototype.toString.call(o)
    .match(/(\w+)\]$/)[1]
    .toLowerCase();
}

checkType({})               // object
checkType([])               // array
checkType(function(){})     // function
checkType(1)                // number
checkType(+'3')             // number
checkType(3+'')             // string
```