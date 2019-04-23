- 注意事项：
1. 所有的偏移量属性都是只读的
2. 如果给元素设置了display:none，则它的偏移量属性都为0
3. 每次访问偏移量属性都需要重新计算
```
<div id="test" style="width:100px; height:100px; margin:10px;"></div>        
<script>
console.time("time");
for(var i = 0; i < 100000; i++){
    var a = test.offsetWidth;
}
console.timeEnd('time');//65.129ms
</script>
```
```
<div id="test" style="width:100px; height:100px; margin:10px;"></div>        
<script>
console.time("time");
var a = test.offsetWidth;
for(var i = 0; i < 100000; i++){
    var b = a;
}
console.timeEnd('time');//1.428ms
</script>
```
由上面代码对比可知，重复访问偏移量属性需要耗费大量的性能，所以要尽量避免重复访问这些属性。如果需要重复访问，则把它们的值保存在变量中，以提高性能