# JS实时监听文本域的变化
>  众所周知，使用 `onchange` 事件来监听文本域的变化是我们在开发中用到的最多的方法。但是， `onchange` 是在文本域失焦时才触发，有时候由于需求的原因，需要我们来实时监听文本域的变化，除了使用`keydown`和`keyup`外，我们还可以:
1. 使用 `onpropertychange` 
```
<input type="text" id="txt">

$("#ysy").bind('input propertychange', function() {  
    console.log(new Date().getTime()); 
});
```
2. 使用 `oninput` 
```
document.getElementById('txt').oninput = function(){
    console.log(this.value);
}
```
> 最后，总结一下`onchange, onpropertychange`和`oninput`之间的异同
1. `onchange`事件与`onpropertychange`事件的区别：`onchange`事件在内容改变（两次内容有可能还是相等的）且失去焦点时触发；`onpropertychange`事件却是实时触发，即每增加或删除一个字符就会触发，通过js改变也会触发该事件，但是该事件IE专有。
2. `oninput`事件与`onpropertychange`事件的区别：`oninput`事件是IE之外的大多数浏览器支持的事件，在value改变时触发，实时的，即每增加或删除一个字符就会触发，然而通过js改变value时，却不会触发；`onpropertychange`事件是任何属性改变都会触发的，而`oninput`却只在value改变时触发，`oninput`要通过`addEventListener()`来注册，`onpropertychange`注册方式跟一般事件一样。（此处都是指在js中动态绑定事件，以实现内容与行为分离）>
3. `oninput`与`onpropertychange`失效的情况：  （1）`oninput`事件：a). 当脚本中改变value时，不会触发；b).从浏览器的自动下拉提示中选取时，不会触发。  （2）`onpropertychange`事件：当input设置为`disable=true`后，onpropertychange不会触发。
