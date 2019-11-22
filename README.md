## My97DatePicker
---
#### 1.注意事项
- My97DatePicker目录是一个整体,不可破坏里面的目录结构,也不可对里面的文件改名,可以改目录名
- 各目录及文件的用途:
> WdatePicker.js 配置文件,在调用的地方仅需使用该文件  
calendar.js 日期库主文件  
目录lang 存放语言文件  
目录skin 存放皮肤的相关文件
- 当WdatePicker.js里的属性:$wdate=true时,在input里加上class="Wdate"就会在选择框右边出现日期图标,如果您不喜欢这个样式,可以把class="Wdate"去掉,另外也可以通过修改skin目录下的WdatePicker.css文件来修改样式
#### 2.功能实例
- 常规调用
```
<script src="WdatePicker.js" type="text/javascript"></script>
<input id="time" type="text" onClick="WdatePicker()" />
```
- 图标触发
```
<script src="WdatePicker.js" type="text/javascript"></script>
<input id="time" type="text" />
// $dp.$ 相当于 document.getElementById
<img src="skin/datePicker.gif" onClick="WdatePicker({el:$dp.$('time')})" width="16" height="22" align="absmiddle" />
```
- 平面展示，选择事件
```
<div id="div1"></div>
<script type="text/javascript">
	WdatePicker({eCont: 'div1',onpicked: function(dp){alert('你选择的日期是:'+dp.cal.getDateStr())}});
</script>
```
- 只能选择今天以前的日期(包括今天)
```
<script src="WdatePicker.js" type="text/javascript"></script>
<input id="time" type="text" class="Wdate" onfocus="WdatePicker({skin: 'whyGreen', maxDate: '%y-%M-%d'})" />
```
- 只能选择今天以后的日期(不包括今天)
```
<script src="WdatePicker.js" type="text/javascript"></script>
<input id="time" type="text" class="Wdate" onFocus="WdatePicker({skin: 'whyGreen', minDate: '%y-%M-#{%d + 1}'})" />
```
- 起止时间，开始日期不能大于截止时间，且都不能大于今天
```
<script src="WdatePicker.js" type="text/javascript"></script>
// $dp.$ 相当于 document.getElementById 函数.  
那么为什么里面的 ' 使用 \' 呢? 那是因为 " 和 ' 都被外围的函数使用了,故使用转义符 \ ,否则会提示JS语法错误.  
所以您在其他地方使用时注意把 \' 改成 " 或者 ' 来使用.  
#F{$dp.$D(\'endtime\')||\'%y-%M-%d\'} 表示当 endtime 为空时, 采用 当前时间 的值作为最大值
<input id="starttime" type="text" class="Wdate" onFocus="WdatePicker({maxDate: '#F{$dp.$D(\'endtime\') || \'%y-%M-%d\'}'})" />
<input id="endtime" type="text" class="Wdate" onFocus="WdatePicker({minDate: '#F{$dp.$D(\'starttime\')}', maxDate: '%y-%M-%d'})" />
```