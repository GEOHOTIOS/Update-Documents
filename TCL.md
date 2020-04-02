# 后台页面
### 1.0.9
- 😄配合硬件V2升级 初始化流程中新增NodeID
# 前台页面
## 硬件层V2大版本
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
### 1.0.0 (要求硬件服务为上一个稳定版本)
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