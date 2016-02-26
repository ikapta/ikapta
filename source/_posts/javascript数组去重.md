title: javascript数组去重
date: 2016-02-26 15:59:47
tags: [javascript,数组去重]
---

本身算法比较薄弱，当年被`acm`一段血虐，至今很少涉及，一想就头疼，平时玩多了也不愿思考，此处记录备忘。
<!-- more --> 
>  1. 数组自身比较法

```
/*
	定义一个新的数组，然后遍历旧的数组，如果新的数组中不包含那个元素，就push进入，最后返回新的数组
    */
Array.prototype.uniqueFun=function(){
	var arr1=[];
	for(var i=0;i<this.length;i++){
		if(arr1.indexOf(this[i])==-1){
			arr1.push(this[i])
		}
	}
	return arr1;
}
```

> 2. hash表法

```
/*
	定义一个hash{}对象，因为一开始hash{}为空，hash[this[i]] == undifine, 所以取反push(),之后某个地址就不为空了，同一个对象都会指向同一个的地址，不向新的数组中插入新数据。
*/
var initArr=[1,2,a,a,mm,mm,c];
Array.prototype.uniqueFun=function(){
	var hash={};
	var arr1=[];
	for(var i=0;i<this.length;i++){
		if(! hash[this[i]]){
			hash[this[i]]=true;
			arr1.push(this[i]);
		}
	}
	return arr1;
}
console.log(initArr.uniqueFun());
```