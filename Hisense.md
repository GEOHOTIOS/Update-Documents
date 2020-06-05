# 后台页面
### 1.0.0
- 💥 实现所有功能
# 前台页面
## 硬件服务V2+ 大版本
### 1.0.6 2020/6/5
- 💥海信UI升级 背景、logo
- 🐛硬件异常的全屏遮罩变为阻止用户有调度行为流程的对话框,即硬件异常后依然可以取件员取件、手动开锁
- 🐛进入维护模式的交互 进入方法:连续点击版本号6次
### 1.0.5 2020/5/27
- 💥增加对登录信息必要参数的判断 缺失报错
- 🔨取归档件，单据列表页面，点击返回回到了首页，应该去上一页
- 🔨调度修复完成后,点击再投一单后页面不能操作了
- 💥判断门关的标识统一使用tag
### 1.0.4
- 🐛只扫描不投递单据开发权限到所有人员
- 🐛loading时隐藏倒计时
- 🐛扫描、投递、取退件的“再投一单”、”继续取退件“放右边
- 🐛设置页面增加倒计时
- 🐛归档箱页面增加倒计时
### 1.0.3
- 🔨获取锁配置列表里面缺少await
### 1.0.2
- 🔨deliver最后一步增加目标仓位判断
### 1.0.1
- 🔨校验封面条码时增加domainname
- 🔨只投递不扫描时 文字提示修改
- 😄新增配置(chunk-config.[hash].js)附加参数 extraDeliverBox
  ````javascript
    extraDeliverBox: {
      codeUniq: false //是否启用条码去重
    } //附加投递柜
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
## 硬件服务V2 大版本
### 1.0.4 (可选更新)
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
- 😄新增读卡器配置(config.js)
  ````javascript
    cardCapture: {
      source: 'InputDevice', //可选值 InputDevice 直接读取输入设备的输入值.HardwareService 硬件服务 
      shakeDelay: 1000 //防抖动 单位ms
    }
  ````
- 💥预先实现了下海信员工卡登陆的功能 待API新增接口及联调测试
### 1.0.3 (基于V3.0 beta版)
- 🐛手动开门优化
- 💥硬件层中间件API升级
  ````text
  [~]GET /v2/cell/{code}?type={type} > GET /v2/cell?code={code}&type={type}
  [~]POST /v2/barcode-scanner > POST /v2/barcode/capture
  [-]/v2/barcode-scanner/activate
  [-]/v2/barcode-scanner/deactivate
  [~]POST /v2/card-reader > POST /v2/card/capture
  [-]/v2/card-reader/activate
  [-]/v2/card-reader/deactivate
  [~]POST /v2/dictation/start > POST /v2/dictation/listen
  [~]POST /v2/dictation/stop > POST /v2/dictation/recognize
  [-]POST /v2/dictation
  [~]PUT /v2/display/{page} > POST /v2/display/show?page={page}
  [-]/v2/gripper/state
  [-]/v2/gripper/position
  [~]GET /v2/io/{tag}/signal > GET /v2/io/signal?tag={tag}
  [~]PUT /v2/io/{tag}/signal > PUT /v2/io/signal?tag={tag}
  [~]GET /v2/io/{tag} > GET /v2/io/port?tag={tag}
  [~]GET /v2/lock > GET /v2/lock/list
  [~]GET /v2/lock/{tag} > GET /v2/lock?tag={tag}
  [~]GET /v2/lock/{tag}/state > GET /v2/lock/state?tag={tag}
  [~]POST /v2/lock/{tag} > POST /v2/lock?tag={tag}
  [~]GET /v2/session/{id} > GET /v2/session?id={id}
  [~]PUT /v2/session/{id} > PUT /v2/session?id={id}
  [~]PATCH /v2/session/{id} > PATCH /v2/session?id={id}
  [~]GET /v2/kv/{key} > GET /v2/kv?key={key}
  [~]PUT /v2/kv/{key}?expiration={expiration} > PUT /v2/kv?key={key}&exp={expiration}
  [~]DELETE /v2/kv/{key} > DELETE /v2/kv?key={key}
  [~]POST /v2/printer > POST /v2/printer/print
  [~]POST /v2/speaker > POST /v2/speaker/play
  [~]DELETE /v2/speaker > DELETE /v2/speaker/play
  [-]/v2/speaker/stop
  [~]POST /v2/speech > POST /v2/speech/speak
  [~]DELETE /v2/speech > DELETE /v2/speech/speak
  [-]/v2/speech/stop
  ````
- 💥新增语音识别和打印服务两个模块(未使用)
- 😄下一版本预告(退件换箱调度升级、操作指引语音提示由硬件接管、退件的任务调度升级)
### 1.0.2
- 🐛 修改扫描流程的异常处理
  ````
    无纸扫描时点击放弃不再次开锁直接返回首页
  ````
### 1.0.1
- 🔨 修改配置文件中校验单据规则的部分 
  ````javascript
  return ['0','1','2','3','4','5','6','7','8','9','A','B','C','D','E','F','G','H','I'].some(item=>String(tag).toUpperCase() === item) && !isNaN(e) && e >= 1 && e <= 9 && !isNaN(r) && r >= 1 && r <= 31;
    变更为
    return ['0','1','2','3','4','5','6','7','8','9','A','B','C','D','E','F','G','H','I'].some(item=>String(tag).toUpperCase() === item) && !isNaN(e) && e >= 0 && e <= 9 && !isNaN(r) && r >= 1 && r <= 31;
    ````  
- 😄 新增附加入口功能的配置(config.js)
  ````javascript
    entries: [
        "overThickness" //超厚流程
    ]
  ````  
- 🔨修复手动输入单号页面点击退件，机械完成后还停留在本页面的问题
### 1.0.0
- 💥 实现所有功能
  

# 手机端页面
### 1.0.3 2020/05/28
- 💥将页面的文字及二维码的配置独立出来 chunk-config.[hash].js
  ````javascript
    qrcode: {
        navTitle: '二维码登录', //导航栏标题
        navRightBar: '帮助', //导航栏右侧文案
        tip: '请在将二维码对准扫码区域',//二维码正下方提示文字
        reload: '重新获取', //刷新按钮文字
        options: { //二维码配置
            autoColor: true, //若为 true, 背景图的主要颜色将作为实点的颜色, 即 colorDark,默认 true
            background: "rgba(0,0,0,0)", //背景
            backgroundColor: "#FFFFFF", //背景颜色
            backgroundDimming: "rgba(0,0,0,0)", //叠加在背景图上的颜色, 在解码有难度的时有一定帮助
            bgSrc: undefined, //背景图片地址
            binarize: false, //若为 true, 图像将被二值化处理, 未指定阈值则使用默认值
            binarizeThreshold: 128, //二值化处理的阈值  (0 < threshold < 255)
            colorDark: "#000000", // 实点的颜色
            colorLight: "#FFFFFF", //空白区的颜色
            correctLevel: 1, //容错级别 0-3
            dotScale: 1, //数据区域点缩小比例  (0 < scale <= 1.0)
            gifBgSrc: undefined, //欲嵌入的背景图 gif 地址,设置后普通的背景图将失效。设置此选项会影响性能
            logoBackgroundColor: "rgba(255,255,255,1)",
            logoCornerRadius: 8, //标识及其边框的圆角半径, 默认为0
            logoMargin: 0, //logo外边距
            logoScale: 0.2, //用于计算 LOGO 大小的值, 过大将导致解码失败, LOGO 尺寸计算公式 logoScale*(size-2*margin)
            logoSrc: undefined, //logo的图片地址
            margin: 20, //二维码整体外边距
            size: 0.5, //尺寸, 长宽一致, 包含外边距 <1 表示比例 >1表示px
            whiteMargin: true,//若设为 true, 背景图外将绘制白色边框
        }
    }
  ````
### 1.0.2
- 🐛移除显示优化 变更为任何时候均允许无条件刷新二维码
- 🐛二维码尺寸减小20%
### 1.0.1
- 😄新增下拉刷新页面的功能
### 1.0.0
- 💥 实现所有功能
