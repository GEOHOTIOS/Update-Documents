# 后台页面
### 1.0.9
- 😄配合硬件V2升级 初始化流程中新增NodeID
# 前台页面
## 硬件服务V2+大版本
### 1.0.2
- 🔨获取锁配置列表里面缺少await
### 1.0.1
- 新增配置(chunk-config.[hash].js)>addition>scanner>resultDelay
  ````javascript
    resultDelay: 30000 //从lp.scanner.completion 到 前端展示出图片列表的时间(方便后期优化加钱) 单位ms 0 或 null表示直接返回
  ````
### 1.0.0
- 🐛编码完成
- 🔨修复测试的问题
- 🔨进出首页均挂起调度并设置适当的优先级
- 😄新增配置(chunk-config.[hash].js)附加参数 repeatResolveConfiguration
    ````javascript
      repeatResolveConfiguration: {
        scenes: ['Scan'], //场景 Scan:扫描
        trigger: 'all' //触发方式 equal: 当lp.error.unresolved的errCode === 要解决的问题的errCode all: 只要lp.error.unresolved就触发 空:表示不处理
      } //自动重复resolve的配置
    ````
- 😄新增配置(chunk-config.[hash].js)附加参数 deviceException
    ````javascript
      deviceException: {
        resolveLimiter: 3, //异常修复重试次数 此处不设置默认为正无穷
        limiter: Infinity //异常预制
      }, //deliver的lp.job.unresolved 的异常重试配置
    ````
- 🐛移除配置(chunk-config.[hash].js)参数 solvableErrors
- 🔨完整的addition参数
  ````javascript
    addition: {
    speech: true, //语音播放
    screen: false, //场景
    record: false, //语音听写
    homeReload: {
      delay: 10 * 1000
    }, //归档消息推送前的配置用于刷新剩余仓位数展示
    gripper: {
      limiterType: 'self', //self 夹子本身的限制 paper 纸张数的限制
      limiterKey: 'gridHeight' //纸张数 paperCount || gridHeight 全部为大于的逻辑
    },
    scanner: {
      errors: ['ER_000096','ER_000101'], //错误
      locks: ['scanner-drawer'] //开哪个锁
    }, //扫描仪错误附加处理 
    deviceException: {
      resolveLimiter: 12000, //异常修复重试次数 此处不设置默认为正无穷
      limiter: Infinity //异常预制
    }, //设备异常
    kvStorage: {
      timeout: 7 * 24 * 60 * 1000
    }, //本地存储的失效时间
    cardCapture: {
      source: 'HardwareService', //可选值 InputDevice 直接读取输入设备的输入值.HardwareService 硬件服务
      shakeDelay: 1000 //防抖动 单位ms
    },
    repeatResolveConfiguration: {
      scenes: ['Scan'], //场景 Scan:扫描
      trigger: 'all' //触发方式 equal: 当lp.error.unresolved的errCode === 要解决的问题的errCode all: 只要lp.error.unresolved就触发 空:表示不处理
    } //自动重复resolve的配置
  },
  ````
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