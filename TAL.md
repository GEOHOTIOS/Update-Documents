# 后台页面
### 1.0.0
- 💥 实现所有功能
# 前台页面
## 硬件服务V2+ 大版本
### 1.0.4 20206/16
- 🐛修复部分情况下可能卡死的问题
- 🐛两处流程问题
- 💥增加非激活状态的ping/pong的处理、增加ping间隔的growfactor
  ```javascript
    websocket: {
      maxReconnectionDelay: 5000, //最大重连间隔
      minReconnectionDelay: 300, //最小重连间隔
      reconnectionDelayGrowFactor: 1.2, //重试间隔成长速度
      connectionTimeout: 5000, //重连超时时间
      defaultHeartCheckDelay: 30 * 1000, //默认心跳检查周期
      heartCheckDelayGrowFactor: 1.5, //心跳检查周期成长速度
      heartCheckTimeout: 3 * 1000 //心跳检查超时时间
    }
  ```
- 💥增加流程日志 增加控制台日志的清理周期设置
  ```javascript
    logger: {
      level: 'trace', //日志级别 可选值: trace debug info warn error
      clearDelay: 7 * 24 * 60 * 1000 //整型值 默认一周 单位ms
    }
  ```
### 1.0.3 2020/6/5
- 🐛遮罩时暂停倒计时,倒计时结束后关闭对话框
- 🐛硬件异常的全屏遮罩变为阻止用户有调度行为流程的对话框,即硬件异常后依然可以取件员取件、手动开锁
- 🐛进入维护模式的交互 进入方法:连续点击版本号6次
### 1.0.2 2020/5/27
- 💥判断门关的标识统一使用tag
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