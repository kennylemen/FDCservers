# Google Play订阅支付接入全指南：服务端验证与后台配置详解

![Google支付配置流程图](https://bbtdd.com/wp-content/uploads/img/4529218855834.webp)

## 一、支付回调配置全流程
### 1.1 创建Pub/Sub主题
1. 访问[Google Cloud Pub/Sub控制台](https://console.cloud.google.com/projectselector2/cloudpubsub/topic/list)
2. 新建主题并配置基本参数
3. 创建订阅时填入服务端回调地址（接收支付成功通知）

![订阅创建示意图](https://bbtdd.com/wp-content/uploads/img/457531231558923.webp)

**核心配置项**：
- 必须添加服务账号 `google-play-developer-notifications@system.gserviceaccount.com`
- 完成配置后通过[创收设置](https://bbtdd.com/yeka)验证通知链路

👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/yeka)

---

## 二、API项目构建与OAuth授权
### 2.1 API项目创建步骤
1. 在[Google API Console](https://console.cloud.google.com/apis)新建专用项目
2. 启用**Google Play Android Developer API**
3. 配置OAuth同意屏幕（授权页面设置）

![API启用示意图](https://bbtdd.com/wp-content/uploads/img/86773330338955.webp)

### 2.2 关键凭证获取
1. 创建Web应用的OAuth客户端ID
2. 记录Client ID和Client Secret
3. 在Google Play后台关联API项目

---

## 三、授权流程与令牌管理
### 3.1 四步获取令牌
mermaid
graph TD
    A[获取Authorization Code] --> B[换取Refresh Token]
    B --> C[生成Access Token]
    C --> D[调用订单查询API]


### 3.2 关键操作节点
**获取Code**：

https://accounts.google.com/o/oauth2/auth?
scope=https://www.googleapis.com/auth/androidpublisher&
response_type=code&
access_type=offline&
redirect_uri={YOUR_URI}&
client_id={CLIENT_ID}


**令牌维护策略**：
- Refresh Token需永久存储（仅初次获取）
- Access Token有效期5分钟，需定期刷新
- 建议建立自动更新机制

---

## 四、支付验证API调用
### 4.1 订单状态查询接口

GET https://androidpublisher.googleapis.com/androidpublisher/v3/applications/{packageName}/purchases/products/{productId}/tokens/{token}

**参数说明**：
- packageName：应用包名
- productId：商品ID
- token：支付凭证
- access_token：当前有效的访问令牌

---

## 五、常见踩坑指南
1. **测试环境配置**：应用需处于封闭测试并通过审核
2. **Firebase项目联动**：会自动同步API项目配置
3. **Token失效场景**：
   - OAuth同意屏幕未发布（测试状态7天有效）
   - 超过6个月未使用
   - 修改开发者账户密码

---

👉 正在为海外服务订阅支付发愁？[野卡](https://bbtdd.com/yeka) 提供一站式解决方案，支持双币卡轻松支付，立即注册享专属优惠码 **ACCPAY**！