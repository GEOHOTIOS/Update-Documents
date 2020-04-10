# 后台页面
### 1.0.9
- 😄配合硬件V2升级 初始化流程中新增NodeID
# 前台页面
## 硬件层V2大版本
### 1.0.3
- 😄新增取归档件时可以连续去多个箱
- 🐛扫描流程异常中无法修复的异常，点击重试和放弃后需要先取消调度。
- 😄新增附加参数 homeReload
    ````javascript
      homeReload: {
        delay: 10 * 1000 //接口重新调用的间隔 ms
      }
    ````
- 😄新增附加参数 gripper
    ````javascript
      gripper: {
         limterType: 'paper', //self 夹子本身的限制 paper 纸张数的限制
         limter: 40 //限制 目前只在paper下生效
      }
    ````
- 😄新增附加参数 scanner
    ````javascript
      scanner: {
        errors: ['ER_000096','ER_000101'], //错误代码
        locks: ['scanner-drawer'] //需要开的锁
      }
    ````
### 1.0.2 
- 🐛扫描页面 62行 
  ````javascript
    -62 if (rs.code === 200) {
    +62 if (rs.code === 200 && rs.data && rs.data.docStatus === 0) {
  ````
- 🔨修复上传参数中缺少girdId的问题
### 1.0.1 (可选更新)
- 🔨修改无法解决的硬件异常依然会调用resolve接口的问题
- 😄新增可解决的错误列表配置(config.js)
  ````javascript
    solvableErrors: [
      "ER_000015",
      "ER_000022",
      "ER_OOOO50",
      "ER_000078"
    ]
  ````
### 1.0.0 (LTS)
- 😄完成TCL V2重构,适配TCL业务流程
- 🐛本地测试全部流程
- 🔨修复测试中的问题
- 😄新增附加功能配置(config.js)
  ````javascript
    addition: {
        speech: true, //语音播放
        screen: false, //辅屏相关
        record: false //语音听写
    }
  ````