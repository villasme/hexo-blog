---
title: moment
date: 2019-09-05 11:35:57
categories: FE
tags:
    - js库
    - momentJS
---
## 设置语言
* moment.locale(String)

|可选值| 介绍
|:-----:|:----:|
|zh-cn | 中文　|

## 操作

Key	|      简写　|
:------|:--------------------
years	| y
quarters	| Q
months	| M
weeks	| w
days	| d
hours	| h
minutes	| m
seconds	| s
milliseconds	| ms

### 加法
* moment().add(１, 'day')   在现在时间上加一天

### 减法
* moment().subtract(１, 'day') 在现在时间上减一天

### 获取开始时间

语法　|  结果 
:------|:--------------------
moment().startOf('year')       |  2019-01-01T00:00:00+08:00 获取今年的第一天
moment().startOf('month')       |   2019-09-01T00:00:00+08:00 　获取这月的第一天
moment().startOf('quarter')     |   2019-07-01T00:00:00+08:00　获取这个季度的第一天
moment().startOf('week')       |  　2019-09-01T00:00:00+08:00　获取这个周的第一天
moment().startOf('isoWeek')  |      set to the first day of this week according to ISO 8601, 12:00 am
moment().startOf('day')          |  2019-09-04T00:00:00+08:00　获取今天０点时刻
moment().startOf('hour')         |   2019-09-04T11:00:00+08:00　获取当前小时开始
moment().startOf('minute')      |   2019-09-04T11:47:00+08:00　获取当前分
moment().startOf('second')      |   2019-09-04T11:48:17+08:00　获取当前秒的时间

### 结束时间
* moment().endOf(String)

## 显示

### 格式化
string | eg 
:-----|----
YYYY | 2019
YY | 19
MM | 09
DD | 28


* moment([年,月,日,时,分,秒,毫秒]) 设置时间
* moment.unix(1318781876) 通过时间戳设置时间
* moment().format('YYYY-MM-DD')

### 常用方法
> TODO:  在时间中月份从0-11  (9月获取的就是8)

|  方法介绍　|  方法　　　| 返回项| 参数
|----------|:---------------------------|------|-------|
|获取当前月多少天|   moment().daysInMonth() |                       天数(Number)||
|是否之前|          moment('2019-09-02').isBefore('2019-09-03')|    true(Boolean)|时间|
|是否相同|          moment('2019-09-02').isSame('2019-09-02')|      true||
|是否之后|          moment('2019-09-02').isAfter('2019-09-01')|     true||
|是否之间|          moment('2019-09-02).isBetween('2019-09-01', '2019-09-03')|true| 两个参数|
|是否闰年|          isLeapYear() |  false | 数组并且一个值moment([2019]).isLeapYear()|
|取值   |           moment().get('year') | | year、month、date、hour、minute、second、millisecond|
|赋值 |             moment().set('year', 2019) | | year、month、date、hour、minute、second、millisecond|
|最大值|            moment.max([a, b, c]).format()| 最大的时间| 数组或者多个参数（moment对象）|
|最小值|            moment.min([a, b, c]).format()| 最大的时间| 数组或者多个参数（moment对象）|
|克隆 |             var a = moment(); var b = a.clone() | 返回复制的moment对象| |