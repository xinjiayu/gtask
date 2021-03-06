# GTask任务系统

---

## 开放接口

---

### 公共参数及返回数据

以下参数均为http header中设置的键/值
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|token|string||是|访问令牌|1.0.0|

返回数据
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|status|number||是|状态码[0:请求成功 1:请求失败]|1.0.0|
|err_code|string||是|错误代码|1.0.0|
|err_msg|string||是|错误信息|1.0.0|
|body|string||是|业务数据json|1.0.0|

---

### 用户认证 - POST /session/token

#### 描述：通过secretKey获取token

请求数据
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|secretKey|string[6-40]||是|访问密钥,在服务端配置文件中设定，长度6-40字符|1.0.0|

返回数据
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|token|string||是|访问令牌|1.0.0|

---

### 创建任务 - POST /task/job

#### 描述：创建任务

请求数据
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|key|string[1-40]||是|任务的唯一key|1.0.0|

---

### 获取任务基本信息 - GET /task/job

#### 描述：获取任务基本信息

请求数据
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|key|string[1-40]||是|任务的唯一key|1.0.0|

返回数据
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|processorsCount|number||是|处理器数量|1.0.0|
|state|number||是|任务状态码|1.0.0|

---

### 删除任务 - DELETE /task/job

#### 描述：删除任务

请求数据
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|key|string[1-40]||是|任务的唯一key|1.0.0|

---

### 运行任务 - Post /task/job/run

#### 描述：运行任务

请求数据
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|key|string[1-40]||是|任务的唯一key|1.0.0|

---

### 创建执行器 - Post /task/job/processor

#### 描述：为任务创建一个执行器

请求数据
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|key|string[1-40]||是|任务的唯一key|1.0.0|
|code|string[1BYTE-1MB]||是|LUA执行代码|1.0.0|
|trigger|number||是|每次触发执行的时间|1.0.0|
|bReset|bool||是|时间计数是否能够被重置|1.0.0|
|bLoop|bool||是|是否循环执行，执行后自动清零时间计数|1.0.0|
|bExit|bool||是|执行后是否退出任务(⚠️是任务不是处理器)|1.0.0|

---

### 广播重置事件 - Patch /task

#### 描述：所有的任务都会收到重置通知

---

### 重置任务 - Patch /task/job

#### 描述：该任务下设置了bReset的处理器将被重置时间计数

请求数据
| 参数 | 类型 | 默认值 | 必填 | 说明 | 最新版本
|---|---|---|---|---|---|
|key|string[1-40]||是|任务的唯一key|1.0.0|
