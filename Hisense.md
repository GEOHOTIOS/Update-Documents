# 后台页面
### 1.0.0
- 💥 实现所有功能
# 前台页面
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
### 1.0.1
- 😄新增下拉刷新页面的功能
### 1.0.0
- 💥 实现所有功能
