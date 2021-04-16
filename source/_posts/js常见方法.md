---
layout: 'n'
title: js常见方法
date: 2020-09-03 11:02:11
excerpt: 归纳一些js中常用方法
tags:
---

<!-- more -->
#### 1. 苹果机不支持日期格式为-的 所以改为"/"
```
function formatStr(str) {
    str=str.replace(/-/g,"/");
    return str;
}
```
#### 2.苹果手机日期兼容问题 
```
/**
* [dateStr 去掉毫秒数 苹果不兼容 如2018-10-2 12:00:00.0改为2018-10-2 12:00:00]
* @param {[string]} str [日期]
* @return {[string]} [日期]
*/
function dateStr(str){
    str=str.slice(0,str.indexOf("."));
    return str;
}
```
#### 3.计算日期相差天数 

```
/**
* [handleDate 处理日期]
* @param {[type]} startDateString [开始日期]
* @param {[type]} endDateString [结束日期]
* @return {[type]} [天数]
*/
function handleDate(startDateString,endDateString){
    var startDate = (new Date( formatStr(startDateString) )).getTime();
    var endDate = (new Date( formatStr(endDateString) )).getTime();
    var day=(startDate-endDate)/1000/(24*3600);
    return day;
}
```
#### 4.统计每个字符出现的次数 

```
    var str='aagggggssssjjjjjj'
    var obj={}
    for(let i=0;i<str.length;i++){
        var key=str.charAt(i)
        if(obj[key]){
            ++obj[key]
        }else{
            obj[key]=0
            ++obj[key]
        }
    }
    console.log(obj)
    var arr=[];
    for(var j in obj){
        arr.push(obj[j])
    }
    console.log(arr)
```
#### 5.交换数组位置 

```
     /**
     * @Author   xqy
     * @交换数组的位置，上移、下移
     * @param    [arr]     [数组]
     * @param    {[index1]}   下标1  
     * @param    {[index2]}   下标2  
     * @return   [arr]  
     */
    function swapItems(arr, index1, index2) {
        arr[index1] = arr.splice(index2, 1, arr[index1])[0];
        return arr;
    }
```
#### 6.写一个函数，对于给定的数组[1,2,3,4,5,6,7,8,9],移除下标为1,3,5，结果为[1,3,5,7,8,9] 

```
function compare(arr){
    return arr.sort((a,b)=>{
        return a<b
    })
}
function del(arr,num){
    let indexs=compare(num);
    console.log(indexs);
    indexs.map(item=>{
        arr.splice(item,1)
    })
    return arr;
}
console.log(del([1,2,3,4,5,6,7,8,9],[1,3,5])) 
```
#### 7.请把两个数组 ['A1', 'A2', 'B1', 'B2', 'C1', 'C2', 'D1', 'D2'] 和 ['A', 'B', 'C', 'D']，合并为 ['A1', 'A2', 'A', 'B1', 'B2', 'B', 'C1', 'C2','C'] 

```
let a1 = ['A1', 'A2', 'B1', 'B2', 'C1', 'C2', 'D1', 'D2']
let a2 = ['A', 'B', 'C', 'D'].map((item) => {
    return item + 3
})

let a3 = [...a1, ...a2].sort().map((item) => {
    if(item.includes('3')){
        return item.split('')[0]
    }
    return item
})
```
#### 8.url参数解析为对象，如http://www.baidu.com?a=1&b=2&c=3解析为{a:1,b:2,c:3} 

```
function handleUrl(url){
    var obj={};
    let params=url.split("?")[1];
    let arr=params.split('&');
    arr.forEach(item=>{
        let a=item.split('=');
        obj[a[0]]=a[1];
    })
    console.log(obj);
    return obj;
}
```
#### 9.求斐波那契数列第ｎ项的值 

```
//方法一
var num1 = 1;
var num2 = 1;
function lie(n){
for(var i = 3; i <= n; i++) {
    var temp = num2;
    num2 = num1 + num2;
    num1 = temp;
}
    return num2;
}
lie(9);

//方法二
function FbDg(n){
    if(n>=3){
        return FbDg(n-2)+FbDg(n-1);
    }else{
        return 1;
    };
};
FbDg(8);
``` 
#### 判断数据类型  
- typeOf 
- instanceOf 
- Object.prototype.toString
