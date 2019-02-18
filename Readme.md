## 模块划分


```mermaid
graph TB

用户 --> 用户明细
用户明细 --> 手机
用户明细 --> 邮箱
用户明细 --> Google
用户明细 --> 昵称 
用户明细 --> 平台密码
用户明细 --> Keybase
Keybase --> github
Keybase --> twitter
Keybase --> reddit
Keybase --> facebook
Keybase --> 钱包地址
Keybase --> other
用户 --> 账户
账户 --> 账户明细
账户 --> 合约
账户明细 --> 公私钥
账户明细 --> 账户类型
账户明细 --> 资产
资产 --> 账本
资产 --> 合约
资产 --> 资产明细
资产明细 --> 类型
资产明细 --> 代码
资产明细 --> 发行地址
资产明细 --> 发行源(属于哪个链)
资产明细 --> 余额1
项目 --> 标注
项目 --> 账户
项目 --> 项目明细
管理员 
通知机制 --> 手机
通知机制 --> 邮件
检验机制 --> 邮件
检验机制 --> Google


```


流程案例：用户验证`
```mermaid

sequenceDiagram
    participant U as 用户
    participant A as 资产
    participant P as 项目

    U->>P: 发起募集
    P->>A: 资本需求

```

流程案例：项目募集
```mermaid

sequenceDiagram
    participant U as 用户
    participant A as 资产
    participant P as 项目

    U->>P: 发起募集
    P->>A: 资本需求

```

流程案例：用户冻结
```mermaid

sequenceDiagram
    participant S as 管理员
    participant A as 资产
    participant P as 项目

    U->>P: 发起募集
    P->>A: 资本需求

```

流程案例：充提资金
```mermaid

sequenceDiagram
    participant S as 管理员
    participant A as 资产
    participant P as 项目

    U->>P: 发起募集
    P->>A: 资本需求

```

