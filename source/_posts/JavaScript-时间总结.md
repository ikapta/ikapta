title: JavaScript 时间总结
date: 2016-05-09 14:04:51
tags: [JavaScript时间]
---
## 获取当前时间 - 时间戳(毫秒)
```
var now =new Date();
now = now.getFullYear() + "/" + (now.getMonth() + 1) + "/" + now.getDate() + ' ' +now.getHours()+':'+now.getMinutes();  //2016/5/8 23:59

//时间戳
var timeStamp= new Date().getTime(); //1462722503341
var timeStamp1=Date.now(); //
var timeStamp2=Date.parse(new Date()) //1462722503341

// 时间戳转时间
var time =new Date(timeStamp); // 此处timeStamp是数字类型 new Date(1462722503341)
time = time.getFullYear() + "/" + (time.getMonth() + 1) + "/" + time.getDate();

//时间转时间戳
var myStamp= new Date('2016/5/8').getTime(); //此处时间是字符串  1462722503341
var myStamp= Date.parse( new Date('2016/5/8') ); //此处时间是字符串  1462722503341


** Date.parse()函数的返回值为 Number类型，返回该字符串所表示的日期与 1970 年 1 月 1 日午夜之间相差的毫秒数。
```
## 计算相差天数
<!-- more -->
```
 function dayDiff(s2,s1){
            s1 = new Date(s1);
            s2 = new Date(s2);
            var time= s2.getTime()-s1.getTime() ;
            var days = parseInt(time / (1000 * 60 * 60 * 24));
            return days;
    }
```

### functions
```

        /**
		 * 毫秒转为yyyy/MM/dd 格式
		 */
		date2Format : function(millisecond){
			if(millisecond ==  null || !millisecond || millisecond ==''){
				return ' ';
			}
			var _this = this;
		    var date = new Date(millisecond);
		    var seperator1 = "/";
		    var month = date.getMonth() + 1;
		    var strDate = date.getDate();
		    if (month >= 1 && month <= 9) {
		        month = "0" + month;
		    }
		    if (strDate >= 0 && strDate <= 9) {
		        strDate = "0" + strDate;
		    }
		    var currentdate = date.getFullYear() + seperator1 + month + seperator1 + strDate;
		    return currentdate;
		}

        /**
		 * 毫秒转为yyyy.MM.dd HH:mm:ss格式
		 */
		dateFormat : function(millisecond){
			if(millisecond ==  null || !millisecond || millisecond ==''){
				return ' ';
			}
			var _this = this;
		    var date = new Date(millisecond);
		    var seperator1 = ".";
		    var seperator2 = ":";
		    var month = date.getMonth() + 1;
		    var strDate = date.getDate();
		    if (month >= 1 && month <= 9) {
		        month = "0" + month;
		    }
		    if (strDate >= 0 && strDate <= 9) {
		        strDate = "0" + strDate;
		    }
		    var temp_hours = date.getHours();
		    var temp_minutes = date.getMinutes();
		    var temp_seconds = date.getSeconds();
		    if (temp_hours >= 0 && temp_hours <= 9) {
		    	temp_hours = "0" + temp_hours;
		    }
		    if (temp_minutes >= 0 && temp_minutes <= 9) {
		    	temp_minutes = "0" + temp_minutes;
		    }
		    if (temp_seconds >= 0 && temp_seconds <= 9) {
		    	temp_seconds = "0" + temp_seconds;
		    }
		    var currentdate = date.getFullYear() + seperator1 + month + seperator1 + strDate
		            + " " + temp_hours + seperator2 + temp_minutes
		            + seperator2 + temp_seconds;
		    return currentdate;

		}
```

## list对象按照时间排序
```
//当万恶的后台返回一个list的时候，竟然是乱序的，你只能自己动手了
//利用JavaScript的原生sort()方法

 json.LIST.sort(function(d1,d2){
                    var date1=new Date(d1.startTime);
                    var date2=new Date(d2.startTime);
                    return Date.parse(date2) - Date.parse(date1);
                });
```
