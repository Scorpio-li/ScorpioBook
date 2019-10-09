## 1. 格式化已过的时间
```js
/**
 * @desc   格式化${startTime}距现在的已过时间
 * @param  {Date} startTime 
 * @return {String}
 */
function formatPassTime(startTime) {
    var currentTime = Date.parse(new Date()),
        time = currentTime - startTime,
        day = parseInt(time / (1000 * 60 * 60 * 24)),
        hour = parseInt(time / (1000 * 60 * 60)),
        min = parseInt(time / (1000 * 60)),
        month = parseInt(day / 30),
        year = parseInt(month / 12);
    if (year) return year + "年前"
    if (month) return month + "个月前"
    if (day) return day + "天前"
    if (hour) return hour + "小时前"
    if (min) return min + "分钟前"
    else return '刚刚'
}
```

## 2. 格式化现在距某个时间的剩余时间
```js
/**
 * 
 * @desc   格式化现在距${endTime}的剩余时间
 * @param  {Date} endTime  
 * @return {String}
 */
function formatRemainTime(endTime) {
    var startDate = new Date(); //开始时间
    var endDate = new Date(endTime); //结束时间
    var t = endDate.getTime() - startDate.getTime(); //时间差
    var d = 0,
        h = 0,
        m = 0,
        s = 0;
    if (t >= 0) {
        d = Math.floor(t / 1000 / 3600 / 24);
        h = Math.floor(t / 1000 / 60 / 60 % 24);
        m = Math.floor(t / 1000 / 60 % 60);
        s = Math.floor(t / 1000 % 60);
    }
    return d + "天 " + h + "小时 " + m + "分钟 " + s + "秒";
}
```

## 3. 获取当前的时间yyyy-MM-dd HH:mm:ss
```js
export default const obtainDate=()=>{
 let date = new Date();
      let year = date.getFullYear();
      let month = date.getMonth() + 1;
      let day=date.getDate();
      let hours=date.getHours();
      let minu=date.getMinutes();
      let second=date.getSeconds();
      //判断是否满10
      let arr=[month,day,hours,minu,second];
      arr.forEach(item=>{
        item< 10?"0"+item:item;
      })
      return year+'-'+arr[0]+'-'+arr[1]+' '+arr[2]+':'+arr[3]+':'+arr[4]      
}
```

## 4. 将时间戳转化为yyyy-MM-dd HH:mm:ss
```js
export default const returnTimestamp=(strTime)=>{
  let middleDate=new Date(strTime)
  return middleDate.toLocaleString('zh-CN',{hour12:false}).replace(/\b\d\b/g, '0$&').replace(new RegExp('/','gm'),'-')
})   
```

## 5. 比较yyyy-MM-dd时间大小
```js
export default const compareTwo=(dateOne,dateTwo)=>{
    return Number(dateOne.replace(/\-/g,""))<Number(dateTwo.replace(/\-/g,""))
}
```

## 6. 计算两个日期格式为(yyyy-MM-dd)相差几个月
```js
export default const disparityFewMonth = (dateOne, dateTwo) => {
    let datesOne = dateOne.split('-').map(item => Number(item));
    let datesTwo = dateTwo.split('-').map(item => Number(item));
    const diff = [0, 0, 0].map((value, index) => {
        return datesOne[index] - datesTwo[index]
    });
    return (diff[0] * 12 + diff[1]) + '月' + diff[2] + '天'
}
```

## 7. new Date对象可接受的参数

```js
/*
1、new Date("month dd,yyyy hh:mm:ss"); 
2、new Date("month dd,yyyy"); 
3、new Date(yyyy,mth,dd,hh,mm,ss); 注意：这种方式下，必须传递整型；
4、new Date(yyyy,mth,dd); 
5、new Date(ms); 注意：ms:是需要创建的时间和
6.new Date(yyyy-MM-dd hh:mm:ss)
GMT时间1970年1月1日之间相差的毫秒数；当前时间与GMT1970.1.1之间的毫秒数：var mills = new Date().getTime();
注意:mth:用整数表示月份，从0（1月）到11（12月）
*/
// 时间格式化
function format_date(timeStamp) {
    let date = new Date(timeStamp);
    return date.getFullYear() + "年"
        + prefix_zero(date.getMonth() + 1) + "月"
        + prefix_zero(date.getDate()) + "日 "
        + prefix_zero(date.getHours()) + ":"
        + prefix_zero(date.getMinutes());
}

// 数字格式化
function prefix_zero(num) {
    return num >= 10 ? num : "0" + num;
}

// 倒计时时间格式化
function format_time(timeStamp) {
    let day = Math.floor(timeStamp / (24 * 3600 * 1000));
    let leave1 = timeStamp % (24 * 3600 * 1000);
    let hours = Math.floor(leave1 / (3600 * 1000));
    let leave2 = leave1 % (3600 * 1000);
    let minutes = Math.floor(leave2 / (60 * 1000));
    let leave3 = leave2 % (60 * 1000);
    let seconds = Math.floor(leave3 / 1000);
    if (day) return day + "天" + hours + "小时" + minutes + "分";
    if (hours) return hours + "小时" + minutes + "分" + seconds + "秒";
    if (minutes) return minutes + "分" + seconds + "秒";
    if (seconds) return seconds + "秒";
    return "时间到！";
}
```


## 8. 获取当前月的最后一天

```js
/*
timeStamp: 时间
*/
// 获取上个月的最后一天
function (timeStamp) {
    let endDate = new Date(timeStamp); // 获取当前时间
    return endDate.setDate(0); // 获取上个月的最后一天(结果是时间戳)
}

// 获取当前月的最后一天
function (timeStamp) {
    var date= new Date(timeStamp); //0 表示1月
    // month + 1，在 JS 中会理解成: 当前日期 + 当月的天数
    date.setDate(28); // 为了保证month + 1 不会多跳过一个月，即1月31号跳到3月的情况，所以统一设置为28号
    date.setMonth(date.getMonth() + 1);
    // 日期设置为0号, 0表示1号的前一天
    let lastDay = date.setDate(0);
    console.log('最后一天：' + new Date(lastDay).toLocaleString()) 
}
```

## 9. 日期校验
```js
/*
*日期校验代码，它允许你自定义日期格式并进行日期有效性的校验。
*参数：
  value:需要教验的日期
  userFormat:自定义的日期格式
*/
function isValidDate(value, userFormat) {

  // Set default format if format is not provided
  userFormat = userFormat || 'mm/dd/yyyy';

  // Find custom delimiter by excluding
  // month, day and year characters
  var delimiter = /[^mdy]/.exec(userFormat)[0];

  // Create an array with month, day and year
  // so we know the format order by index
  var theFormat = userFormat.split(delimiter);

  // Create array from user date
  var theDate = value.split(delimiter);

  function isDate(date, format) {
    var m, d, y, i = 0, len = format.length, f;
    for (i; i < len; i++) {
      f = format[i];
      if (/m/.test(f)) m = date[i];
      if (/d/.test(f)) d = date[i];
      if (/y/.test(f)) y = date[i];
    }
    return (
      m > 0 && m < 13 &&
      y && y.length === 4 &&
      d > 0 &&
      // Check if it's a valid day of the month
      d <= (new Date(y, m, 0)).getDate()
    );
  }

  return isDate(theDate, theFormat);
}



// 使用方法
console.log(isValidDate('34/2/2012','dd/mm/yyyy'));
```

## 10.倒计时

```js
/**
 * @author xiaojue
 * @date 20160420
 * @fileoverview 倒计时想太多版
 timeDate: 想要倒计时的时间参数
 */
function countdown_time(timeDate) {

  function timer(delay) {
    this._queue = [];
    this.stop = false;
    this._createTimer(delay);
  }

  timer.prototype = {
    constructor: timer,
    _createTimer: function(delay) {
      var self = this;
      var first = true;
      (function() {
        var s = new Date();
        for (var i = 0; i < self._queue.length; i++) {
          self._queue[i]();
        }
        if (!self.stop) {
          var cost = new Date() - s;
          delay = first ? delay : ((cost > delay) ? cost - delay : delay);
          setTimeout(arguments.callee, delay);
        }
      })();
      first = false;
    },
    add: function(cb) {
      this._queue.push(cb);
      this.stop = false;
      return this._queue.length - 1;
    },
    remove: function(index) {
      this._queue.splice(index, 1);
      if(!this._queue.length){
        this.stop = true;
      }
    }
  };

  function TimePool(){
    this._pool = {}; 
  }

  TimePool.prototype = {
    constructor:TimePool,
    getTimer:function(delayTime){
      var t = this._pool[delayTime];
      return t ? t : (this._pool[delayTime] = new timer(delayTime));
    },
    removeTimer:function(delayTime){
      if(this._pool[delayTime]){
        delete this._pool[delayTime];
      }
    }
  };

  var delayTime = 1000;
  var msInterval = new TimePool().getTimer(delayTime);

  function countDown(config) {
    var defaultOptions = {
      fixNow: 3 * 1000,
      fixNowDate: false,
      now: new Date().valueOf(),
      template: '{d}:{h}:{m}:{s}',
      render: function(outstring) {
        console.log(outstring);
      },
      end: function() {
        console.log('the end!');
      },
      endTime: new Date().valueOf() + 5 * 1000 * 60
    };
    for (var i in defaultOptions) {
      if (defaultOptions.hasOwnProperty(i)) {
        this[i] = config[i] || defaultOptions[i];
      }
    }
    this.init();
  }

  countDown.prototype = {
    constructor: countDown,
    init: function() {
      var self = this;
      if (this.fixNowDate) {
        var fix = new timer(this.fixNow);
        fix.add(function() {
          self.getNowTime(function(now) {
            self.now = now;
          });
        });
      }
      var index = msInterval.add(function() {
        self.now += delayTime;
        if (self.now >= self.endTime) {
          msInterval.remove(index);
          self.end();
        } else {
          self.render(self.getOutString());
        }
      });
    },
    getBetween: function() {
      return _formatTime(this.endTime - this.now);
    },
    getOutString: function() {
      var between = this.getBetween();
      return this.template.replace(/{(\w*)}/g, function(m, key) {
        return between.hasOwnProperty(key) ? between[key] : "";
      });
    },
    getNowTime: function(cb) {
      var xhr = new XMLHttpRequest();
      xhr.open('get', '/', true);
      xhr.onreadystatechange = function() {
        if (xhr.readyState === 3) {
          var now = xhr.getResponseHeader('Date');
          cb(new Date(now).valueOf());
          xhr.abort();
        }
      };
      xhr.send(null);
    }
  };

  function _cover(num) {
    var n = parseInt(num, 10);
    return n < 10 ? '0' + n : n;
  }

  function _formatTime(ms) {
    var s = ms / 1000,
      m = s / 60;
    return {
      d: _cover(m / 60 / 24),
      h: _cover(m / 60 % 24),
      m: _cover(m % 60),
      s: _cover(s % 60)
    };
  }

  var now = Date.now();

  // new countDown({});
  new countDown({
    endTime: now + timeDate * 1000
  });

};

countdown_time(20);
```

## 11.时间格式化

- 参数：
    
    1. oldDate 类型可以是 Date，String，Number。

    2. fmt 是格式化的类型：yyyy-MM-dd hh:mm，其中的 yyyy | MM | dd | hh | mm 是分别匹配 年 | 月 | 日 | 时 | 分 的关键字。其中的连字符是可以随意替换的，只展示年月将其他关键字去掉即可。

```js
export function formatDate (oldDate, fmt) {  
  let date = new Date()  
  if (typeof oldDate === 'string' || typeof oldDate === 'number') {    
    date = new Date(+oldDate)  
  } else {    
    date = oldDate  
  }  
if (/(y+)/.test(fmt)) {    
  fmt = fmt.replace(RegExp.$1, (date.getFullYear() + '').substr(4 - RegExp.$1.length))  }  
  let o = {    
  'M+': date.getMonth() + 1,    
  'd+': date.getDate(),    
  'h+': date.getHours(),    
  'm+': date.getMinutes(),    
  's+': date.getSeconds()  }  
  function padLeftZero (str) {    
    return ('00' + str).substr(str.length)  
  }  
  for (let k in o) {    
    if (new RegExp(`(${k})`).test(fmt)) {      
      let str = o[k] + ''      
      fmt = fmt.replace(RegExp.$1, (RegExp.$1.length === 1) ? str : padLeftZero(str))    
    }  
  }  
  return fmt
}
/*
yyyy年MM月dd -> 2019年09月7日
hh分mm秒 -> 16分53秒
*/
```

## 12.以“天”为单位获取响应的时间戳

```js
export function setDate(num) {  return Date.now() + num * 24 * 60 * 60 * 1000}
/*
eg: 
12 个小时之前的时间 -> setDate(-.5)
24 个小时之前的时间 -> setDate(-1)
三天后的时间 -> setDate(3)
*/
```