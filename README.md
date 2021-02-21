# JumpyDumpty  

**蹦蹦炸弹——原神小工具箱**

 Electron + Vue + AntDesign

 新手尝试，还有很多不足的地方

## 功能：  

 - 热键资源地图

    由于平时在探索地图找资源时（如神瞳，特产，宝箱），需要用浏览器打开资源地图对照着来找，但如果频繁切换窗口会过于麻烦，就算用Alt+Tab也有闪烁，于是弄了这个热键呼出地图的小工具。

    默认加载米游社观测枢的地图，游戏中的标点可同步
    支持独立地图的热键呼出和隐藏

    呼出地图窗口后，由于原神从游戏切换其他窗口默认会最小化，隐藏地图窗口时调用了windows api的函数重新激活原神窗口，从而实现近似于游戏地图的体验


 - 角色查询 
 
    刷新观测枢地图时，用Electron的webRequest功能拦截headers，获取cookie
    
    查询的API和方法源自于GitHub上的各位大佬

 - 圣遗物OCR导出（测试中）
  
    依赖：百度OCR的API，需要提供百度OCR的相关Key。获取方法：登录官网创建OCR应用即可[点我打开官网](https://login.bce.baidu.com/)
 
    运行条件：

     - 管理员权限(无权限只能手动抓取)
     - 游戏必须保持前台，即使是独占全屏也可以（但全屏下不能看到其他窗口消息，不太建议）
     - 分辨率必须为16：9，如3840×2160，2560X1440，1920×1080，1600×900，1366×768，1280×720

   建议窗口模式下运行，分辨率越高越好（测试在1280*720的情况下，百度OCR少数结果存在漏掉百分号或者逗号甚至数字的情况），Api建议使用高精度版（每天500次，应该没人会用完吧）

   使用方法：
     - 运行程序，先输入你的ApiKey和SecretKey，点击获取AccessToken
     - 可手动点击按钮抓取
     - 默认注册热键为Alt+R，按下该热键后，开启快速抓取模式，程序自动抓取鼠标点击事件来抓取游戏屏幕并OCR识别（此时只需要逐个点击背包的圣遗物即可）

   注意事项：
     - 快速抓取模式下可以进行鼠标拖动（可以随便拖动背包界面），仅鼠标点击会被判定为有效。
     - 不要尝试在同一个圣遗物的详细界面多次点击鼠标，会重复录入
     - 快速抓取模式下的点击不要太快，百度api默认限制1秒两次请求
     - 相关功能还在完善......


## 使用：  
v1.0.4,v1.0.5beta已打包，解压直接运行：  
https://wws.lanzous.com/b01zxfq8j
密码:boom

## 更新日志：  

### v1.0.5beta
 - 增加圣遗物OCR导出功能，仅支持导出为json格式

### v1.0.4
 - 优化查询界面
 - 增加读取Cookie时，查询数据时的通知提醒框
  
### v1.0.3
 - 完善角色查询的深渊查询

### v1.0.2
 - 增加角色查询
 - 可指定设置Cookie
 - 增加自动读取 刷新米游社观测枢地图 时的Cookie的功能
  
### v1.0.1
 - 增加自定义热键
 - 优化切换回游戏窗口造成的闪烁
 - 优化禁止多开

### v1.0.0
 - 初始版本  

 - 地图预览功能
 - 通过热键打开独立地图  





