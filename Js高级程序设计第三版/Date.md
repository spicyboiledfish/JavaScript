### 关于Date类型的一些常用API
	
> 创建Date对象

1. 可以不传参数，返回值是当前时间 <code>var date = new Date();</code> 

2. 可以传参数，以指定的时间创建日期

3. 此时必须传入指定时间的毫秒

4. 于是有了下面两个方法将传入的日期转换为毫秒数

<code>Date.parse("表示日期的字符串参数")</code>
<code>Date.UTC()</code>

5. 如果传入的字符串不能表示日期，那么会返回NAN

6. 实际上，可以直接将字符串传给Date，后台会默认调用<code>Date.parse()</code>

7. <code>Date.UTC()</code>传入的参数是年月日时分秒，年月是必须的, 月是基于0的。

8. 同样，直接向Date里传入年月日时分秒也可以，不过和传入<code>Date.parse()</code>有区别。

9. IE9+以及其他浏览器支持<code>Date.now()</code>, 返回当前时间的毫秒数， 

10. 不支持Date.now()的方法的浏览器，可以使用+操作符将Date对象转换为字符串，可以达到同样的目的。

11. UTC(Universal Time Coordinated) + 时区差 = 本地时间

12. 在没有时间误差的情况下，UTC=GTM, 都是和英国伦敦本地时间一样

```
// 1.
var date1 = new Date();

// 2.
var date2 = new Date(Date.parse("May 25, 2016"));

// 3.
var date3 = new Date("May 25, 2016");

// 4. GMT时间2000年1月
var date4 = new Date(Date.UTC(2000, 0)); 

// 5. GMT时间2000年1月1日上午9点12分12秒
// 转换为本地时间就是2000年1月1日17点12分12秒
var date5 = new Date(Date.UTC(2000, 1, 1, 9, 12, 12));

// 6. 本地时间2000年1月
var date6 = new Date(2000, 0);

// 7. 本地时间2000年1月1日上午9点12秒12分
var date7 = new Date(2000, 0, 1, 9, 12, 12);

// 8. 获取当前时间
var date8 = Date.now();

// 9. 不支持Date.now()的浏览器使用的方法
var date9 = +new Date();
```


> 日期格式化方法


因为现在涉及到的是只是中国,所以没有考虑这个


> 日期/时间组件方法

```
// 返回日期的毫秒数;与valueOf()方法的返回值相同
var date = new Date().getTime();
var date1 = new Date().valueOf();

// 设置日期的毫秒数
setTime(毫秒数)

// 设置和获取年(4位)

getFullYear()
setFullYear()

// 设置和获取月(以0为1月)
setMonth()
getMonth()

// 设置和获取日
getDate()
setDate()

// 获取星期(以0为星期1)
getDay()

// 设置和获取小时(以0为1点,0~23)
getHour()
setHour()

// 设置和获取分(以0为1分，0~59) 
setMinutes()
getMinutes()

// 设置和获取秒(以0为1秒，0~59)
setSeconds()
getSeconds()

// 设置 和获取日期中的毫秒
setMilliseconds()
getMilliseconds()


// 以上方法都有UTC的方法，除了getTime和setTime

```


















