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

