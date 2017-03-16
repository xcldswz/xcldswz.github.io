---
layout: post
title:  "DIY智能温湿度计（下）之APP控制"
date:   2017-03-16 19:06:05
categories: Arduino
excerpt: 硬件相关。
---

* content
{:toc}

# 一、工具
## 1、Arduino UNO



## 2、HC-05蓝牙参数（数据来自七星虫官网）

![HC-05](http://upload-images.jianshu.io/upload_images/3845101-543e09e43f4019f3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 采用CSR主流蓝牙芯片，蓝牙V2.0协议标准*

* 串口模块工作默认电压3.6~6V。*

* 波特率为4800，9600,19200，38400，57600，115200用户可设置。默认9600*

* 核心模块尺寸大小为：28mm x 15 mm x 2.35mm。*

* 工作电流：配对中：30～40mA配对完毕未通信：2～8mA 。通信中：8mA*

* 休眠电流：无休眠*
## 3、DHT11
## 4、Android手机
## 5、[蓝牙串口助手](http://pan.baidu.com/s/1eRLf18u)（Android版点击即可下载，iOS版暂时不提供）
>蓝牙串口助手是一款基于RFCOMM蓝牙串口服务的传输软件，通过该软件可以连接蓝牙串口模块进行通信，实现手机串口连接。类似计算机的串口助手，是电子工程师的开发利器

# 三、接线
1、DHT11的S、+、-接口分别接Arduino的引脚4（可以根据自己的需要选择其他引脚）、5V、GND。
2、蓝牙RXD、TXD、VCC、GND分别接Arduino的TXD、RXD、5V、GND（千万不要弄混哟，RXD-->TXD）

![dht_wire.jpg](http://upload-images.jianshu.io/upload_images/3845101-db980dc568f670ba.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# 四、编程
## 1、功能

程序可以获取当前环境温湿度，并通过蓝牙将数据实时传送到Android手机APP中，打开APP就可以显示。

## 2、代码
```
#include<dht.h>
#define DHT11_PIN 4//定义dht11信号线S为引脚4
dht DHT;

void setup()
{
Serial.begin(9600);//初始化端口
}

//循环
void loop()
{
int val=Serial.read();//读取串行端口的值
switch (val)
{
//如果手机端输入“T”，则执行wsd()函数。（T可以根据自身需要修改，但要与APP端同步）
  case 'T': wsd();break;
}

}
void wsd()//定义温湿度函数
{
  //分别显示测量湿度、温度值
int chk = DHT.read11(DHT11_PIN);//读取传感器获取的数据
//在串口输出湿度和温度的单位分别是%和C（摄氏度）
Serial.println("Type,\tstatus,\tHumidity (%),\tTemperature (C)");
Serial.print(DHT.humidity,1);
Serial.print(",\t");
Serial.println(DHT.temperature,1);
delay(1000);//延时1s
}
```
## 3、手机端操作
安装并打开蓝牙串口助手App（Android版），设置好后显示蓝牙连接成功后，会出现下面的效果（篇幅有限具体APP使用方法请参照文章[蓝牙串口助手使用方法](http://www.jianshu.com/p/95480df195b9)）
![蓝牙连接成功](http://upload-images.jianshu.io/upload_images/3845101-00f03548cc1119a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
点击“温度”按钮，就会出现实验结果
![app_result.png](http://upload-images.jianshu.io/upload_images/3845101-5df9a249fedc13ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 五、用途
1、蓝牙用途：可用于GPS导航系统，水电煤气抄表系统等
2、智能温湿度计用途：集娱乐性和实用性于一体。可以通过手机APP实时获取当前环境准确温湿度信息，可以用于节水农业灌溉、温室大棚等等

# 六、拓展
1、视觉上：可以在原有系统内加入红色LED和蓝色LED小灯，如果温度过高这控制红灯亮，如果温度过低则蓝灯亮
2、听觉上：可以加入蜂鸣器，温度过高或过低即可发出警报
视觉与听觉相结合的智能温湿度计是不是更加有意思，有没有亲自动手做一个的欲望！请关注我的下一篇文章《DIY智能温湿度计升级篇》，到时候我还会附上源代码。


# 参考来源：
1.[Arduino官方网站](http://arduino.cc/)
2.[Arduino中文社区](http://www.arduino.cn/)