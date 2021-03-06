title: 基于野火Server服务端二次开发，增加钱包功能设计说明
author: lichongbing
date: 2021-05-10 23:34:29
tags:
---
## 基于野火Server服务端二次开发，增加钱包功能设计说明

### 前言

我们基于野火Server服务端二次开发，在已有IM服务功能上增加好友之间转账功能，陌生人之间扫码转账和收帐，添加零钱功能，我们这个零钱可以用来支付，转账，还可以提现，为此还需实现钱包明细查询，为了保证支付安全，我们会设置交易安全密码。支付服务采用php开发，已经实现，实现支付宝轮训收款。交易支付，钱包是一个基础服务，可以增强我们的IM通信的使用价值，实现商业机会。
<!--more-->

### 源码地址

https://github.com/wildfirechat/server

### 熟悉系统架构设计

![IMG_2957](https://image.lichongbing.com/IMG_2957.PNG)

![IMG_2956](https://image.lichongbing.com/IMG_2956.PNG)

#### 登录

![https://docs.wildfirechat.cn/architecture/login_flow1.png](https://docs.wildfirechat.cn/architecture/login_flow1.png)

### 注册用户

![https://docs.wildfirechat.cn/architecture/register_flow1.png](https://docs.wildfirechat.cn/architecture/register_flow1.png)

### 钱包功能接口设计

#### 规划评估

![IMG_2961](https://image.lichongbing.com/IMG_2961.PNG)


#### 好友转账
1、	功能描述
用户通过客户端用户聊天界面，触摸按钮转账，在弹出的转账界面中输入转账金额与支付密码进行转账。
2、	用例说明	
用例编号	A001
用例名称	好友转账
用例描述	用户通过客户端用户聊天界面，触摸按钮转账，在弹出的转账界面中输入转账金额与支付密码进行转账。
使用者	客户端使用者
触发器	触摸按钮转账
前置条件	用户已经登陆 
基本路径	1输入转账金额与支付密码
2系统处理用户请求，用户成功转账
扩充路径	无
后置条件	功能执行完毕
特殊要求	无


#### 陌生人转账
1、	功能描述
用户通过客户端扫一扫，扫码收款码，在弹出的转账界面中输入转账金额与支付密码进行转账。
2、	用例说明	
用例编号	A002
用例名称	陌生人转账
用例描述	用户通过客户端扫一扫，触摸按钮转账，在弹出的转账界面中输入转账金额与支付密码进行转账。
使用者	客户端使用者
触发器	触摸按钮转账
前置条件	用户已经登陆 
基本路径	1输入转账金额与支付密码
2系统处理用户请求，用户成功转账
扩充路径	无
后置条件	功能执行完毕
特殊要求	无

#### 零钱充值
1、	功能描述
用户通过客户端我的钱包，按充值按钮，在弹出的转账界面中输入充值金额和充值渠道方式充值。
2、	用例说明	
用例编号	A003
用例名称	充值
用例描述	用户通过客户端我的钱包，按充值按钮，在弹出的转账界面中输入充值金额和充值渠道方式充值。
使用者	客户端使用者
触发器	充值按充值
前置条件	用户已经登陆 
基本路径	1输入转账金额与支付密码
2系统处理用户请求，用户成功转账
扩充路径	无
后置条件	功能执行完毕
特殊要求	无

·····

#### swagger api 设计

![IMG_2960](https://image.lichongbing.com/IMG_2960.PNG)


#### 移动端设计

ios andorid 基于原生已经开源，增加二次开发。样式参考微信，自由发挥。