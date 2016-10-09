LCalendar v1.71移动端日期时间选择控件
==========
纯原生js的移动端日期插件，不依赖任何库，体积非常小只有10k
##用法
在html页面中引入input标签，通过自定义属性`data-lcalendar`控制最小日期和最大日期，写法如下：
```
...
<input type="text" readonly="" name="input_date" placeholder="请输入日期" data-lcalendar="2000-01-01,2018-01-29" />
...
```
将样式文件引入到页面中：
```
...
<link rel="stylesheet" href="LCalendar.css">
...
```
同时引入js文件到页面中：
```
...
<script src="LCalendar.js"></script>
...
```
初始化插件：
```
...
var calendar = new LCalendar();
calendar.init({
    'trigger': '#demo1',//标签id
    'type': 'date',//date 调出日期选择 datetime 调出日期时间选择 time 调出时间选择 ym 调出年月选择
    'minDate':'1900-1-1',//最小日期 注意：该值会覆盖标签内定义的日期范围
    'maxDate':'2016-3-18'//最大日期 注意：该值会覆盖标签内定义的日期范围
});
...
```
调用起来非常简单，代码我后续会持续优化，如果喜欢希望赏颗星哦。

### 使用时遇见的bug(滑动过程中，没有停止就确定会报错)
解决办法:
将js文件中的取消方法(line 689~702)修改一下:
```
function closeMobileCalendar(e) {
    e.preventDefault();
    var evt;
    try {
        evt = new CustomEvent('input');
    } catch (e) {
        //兼容旧浏览器(注意：该方法已从最新的web标准中删除)
        evt = document.createEvent('Event');
        evt.initEvent('input', true, true);
    }
    _self.trigger.dispatchEvent(evt);
    document.body.removeChild(_self.gearDate);
    _self.gearDate=null;
}
```
将上面代码修改为以下代码:
```
function closeMobileCalendar(e) {
    e.preventDefault();
    var evt = new CustomEvent('input');
    _self.trigger.dispatchEvent(evt);
    document.body.removeChild(_self.gearDate);
}
```


