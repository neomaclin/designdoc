## 模块划分


```mermaid
graph TB

用户 --> 用户明细
用户 --> 账户
账户 --> 公私钥
资产 --> 账本
资产 --> 合约
项目 --> 标注
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

