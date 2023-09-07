---
outline: deep
---

**服务区域是设置 Agent 监控外部网站或服务器的功能设置区**  
**设置好的服务监控可以在主页中的 “服务” 页查看监控结果**
<br/>

## 使用方法

如需新增一个监控，可以进入管理面板中的 “服务” 页，点击“添加监控”  

新增一个服务监控，你需要设置以下参数：  
+ `名称` - 自定义一个名称  

+ `类型` - 选择一个监控类型，目前哪吒监控支持三种监控类型，分别是 “HTTP-GET”、“ICMP-Ping” 和 “TCP-Ping”

+ `目标` - 根据你选择的类型不同，目标的设置方法也不同
> + `HTTP-GET`: 选择此类型，你应该输入一个URL作为目标，URL需添加 `http://` 或 `https://` **如果你的目标URL是 `https://` ,将会同时监控该URL的SSL证书，当SSL证书到期或发生变更，会触发提醒**  
例如： https://example.com  

> + `ICMP-Ping`: 选择此类型时，你应该输入一个域名或IP，不含端口号  
例如：1.1.1.1 或 example.com 

> + `TCP-Ping`: 选择此类型时，你应该输入一个域名或IP并包含端口号  
例如：1.1.1.1:80 或 example.com:22  

+ `请求间隔`： 设定 Agent 每次请求目标的时间间隔，以秒为单位  

+ `覆盖范围`： 选择一条规则来确定要使用哪些 Agent 来请求目标  

+ `特定服务器`： 配合覆盖范围使用，选择规则内需要排除的 Agent  

+ `通知方式组`： 选择你已经在 “报警” 页设置好的通知方式，[点击这里](/guide/notifications.html#灵活的通知方式)了解详情

+ `启用故障通知`： 根据需要选择是否接收目标故障通知，默认为不勾选  

设置完成后，点击 “添加” 即可  
稍等片刻前往主页的 “服务” 页，查看监控结果
<br/>

## 延迟变化报警
哪吒监控可以监测并统计 Agent 到目标服务器之间的延迟，在发生较大变化的情况下发送通知    
利用此功能可以帮助你监控服务器的线路是否发生了变化  

+ `启用延迟通知`： 开启时，当 Agent 至目标服务器的延迟大于`最高延迟`或小于`最低延迟`时，将会发送报警通知  
<br/>

## 管理监控
如需对已有的服务监控进行管理，可以前往管理面板中的 “服务” 页  
选择一条监控配置，点击右侧的图标进行编辑或删除