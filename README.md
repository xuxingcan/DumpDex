# DumpDex

> 本插件可dump出解密后的Dex文件,支持市面上大多数加密壳,软件仅供学习用，请勿用于其他用途！！！

## 背景

目前大多数加固方式（Dex2C除外）核心原理都是隐藏Dex文件，运行时动态解析出Dex并加载代码。通常破解加固的方式有2种：

### 破解方式一：静态分析加固代码
静态分析存在的问题是每个加固方案都需要去研究加固的代码，导致成本过高。若某一加固方式升级了加固代码，则又需要重新破解。、

### 破解方式二：动态获取Dex
无论如何加固，最终都会解析出Dex并加载。  
此方案早期比较出名的思路有hook关键方案，截取解析出的落地Dex，但随着加固方案的升级，目前几乎所有的加固方案都不会再落地Dex了。  
紧接着，一些Native破解方案被研究出来，通过获取内存中Dex地址偏移量，从内存中dump出完整Dex，此方案存在的问题是各个Android版本以及各个厂商可能都会对源码进行修改，进而导致偏移量计算适配成本较高。  

## 原理
本方案原理和破解方式二一致，通过阅读源码，发现可以通过java层dexCache获取解密后内存中的dex，优点是不需要自己计算偏移量，缺点是Android源码中早已将此方法隐藏。  
本方案通过修改Android源码，将上述隐藏的方法暴露出来，在加密apk运行后，动态获取内存中的Dex。  
诚然，此方案的成本仍较大，需要修改源码并编译刷机，但好在较为稳定，源码修改量不大，也就几十行代码，也不需要深入研究偏移量，后续升级Android版本也不会增加工作量。

## 写在最后
整体方案流程较多，对于初级程序员较为负责，我还在撰写方案文档。
### 大家如果对方案感兴趣，或者手上有加固的APK亟需破解出Dex，可以加我VX：xgcc01，我会免费帮忙破解，也当测试了！
