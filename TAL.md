# 后台页面
### 1.0.0
- 💥 实现所有功能
# 前台页面
## 硬件服务V2+ 大版本
### 1.0.1
- 🔨获取锁配置列表里面缺少await
### 1.0.0
- 🔨deliver最后一步增加目标仓位判断
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
- 😄新增配置(chunk-config.[hash].js)附加参数 extraDoors
    ````javascript
      extraDoors: {
        deliver: 'DELIVER', //投递口
        pickup: 'PICKUP' //取件口 不需要配置 再API那里配置即可
      }, //附件投递柜仓门配置
    ````
- 😄新增配置(chunk-config.[hash].js)附加参数 deviceException
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