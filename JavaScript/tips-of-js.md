### 获取json的 "key" 值
> `var obj = { name: "naruto", age: 23, dad: "minato"}`
1. 使用 `for in` 来循环 :
```
for (var key in obj){
    console.log(key) // 依次输出 "name", "age", "dad"
}
```
- 这种方法比较常见，相信大家看到这个问题时第一时间都会想到吧，但是我要介绍的是下面这个更简单的方法。
2. 使用 `Object.keys()` 来获取 :
```
- console.log( Object.keys(obj) ) // 输出一个数组 ["name", "age", "dad"]
- 所以, 当我们需要某个key值时可以从当前数组中取得。
```
