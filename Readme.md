# 源铸产品设计
## 一、模块划分


```mermaid
graph TB

用户 --> 用户明细
用户 --> 账户
用户 --> 检验机制
用户 --> 通知机制
账户 --> 账户明细
账户 --> 资产
资产 --> 账本
资产 --> 资产明细
项目 --> 标注
账户 --> 项目
项目 --> 项目明细
项目 --> 项目管理
管理员
通知机制 --> 手机
通知机制 --> 邮件
检验机制 --> 邮件
检验机制 --> Google
检验机制 --> keybase
链上账户 --> 在线账户(热)
链上账户 --> 离线账户(冷)
链上账户 --> 新资产账户
链上账户 --> 网络手续费账户
```

## 二、流程案例

流程案例：用户登记
```mermaid

sequenceDiagram
    participant u as 用户
    participant p as 手机
    participant m as 邮箱
    participant a as 账户

    u->>p: 手机登记
    p->>m: 邮箱登记
    m->>u: 验证码检验
    p->>u: 验证码检验
    u->u: 密码登记
    u-->>a: 登记默认账户
    m-->>u: 通知
    p-->>u: 通知
    Note right of a: 普通账户类型

```

流程案例：用户密码重置
```mermaid

sequenceDiagram
    participant u as 用户
    participant p as 手机
    participant m as 邮箱

    u->>p: 手机登记
    p->>m: 邮箱登记
    m->>u: 验证码检验
    p->>u: 验证码检验
    u->>u: 密码重置
    m-->>u: 通知
    p-->>u: 通知

```

流程案例：用户冻结
```mermaid

sequenceDiagram
    participant s as 管理员
    participant u as 用户
    participant a as 账户
    participant p as 手机
    participant m as 邮箱

    s->>u: 冻结
    u->>u: 指定账户或默认全部账户
    u-->>a: 冻结
    m-->>u: 通知
    p-->>u: 通知

```

流程案例：用户解冻
```mermaid

sequenceDiagram
    participant s as 管理员
    participant u as 用户
    participant a as 账户
    participant p as 手机
    participant m as 邮箱

    s->>u: 解冻
    u->>u: 指定解冻账户或默认全部冻结账户
    u-->>a: 解冻
    m-->>u: 通知
    p-->>u: 通知

```

流程案例：用户检验信息解绑
```mermaid

sequenceDiagram
    participant s as 管理员
    participant u as 用户
    participant g as google
    participant p as 手机
    participant m as 邮箱

    s->>u: 选择解绑
    activate u
    alt 解绑谷歌
        u-->>g: 解绑
    else 解绑手机
        u-->>p: 解绑
    else 解绑邮箱
        u-->>m: 解绑
    end
```

流程案例：在线钱包(热)&离线钱包(冷)
```mermaid

sequenceDiagram
    participant ha as 在线钱包(热)
    participant su as 管理员
    participant ca as 离线钱包(冷)

    loop 每日10:00AM
        alt 在线钱包(热)大于总额度1%
            ha -->> su: 划转通知
            ha -->> ha: 多签检验(threshold=2)
            su ->> ca: 划转
        else 离线钱包(冷)大于总额度99%
            ca -->> su: 划转通知
            ca -->> ca: 多签检验(threshold=6)
            su ->> ha: 划转
        end
    end
```

流程案例：资产发行
```mermaid

sequenceDiagram
    participant u as 用户
    participant s as 资产
    participant a as 用户账户
    participant ca as 资产发行账户(链上)
    participant na as 新资产账户(链上)
    participant p as 手机
    participant m as 邮箱

    u->>s: 发行资产
    s-->>ca: 发行
    ca-->>na: 划转
    ca-->>ca: 账户权限死锁
    a-->>a: 90%资产入账
    Note right of a:10%资产作为发行<br>佣金
    p-->>u: 通知
    m-->>u: 通知
```

流程案例：充值
```mermaid

sequenceDiagram
    participant u as 用户
    participant a as 用户账户
    participant ha as 在线账户(热)
    participant p as 手机
    participant m as 邮箱

    u->>a: 充值
    ha-->>ha: 到账检验
    ha-->>a: 余额映射
    p-->>u: 通知
    m-->>u: 通知
```

流程案例：提币
```mermaid

sequenceDiagram
    participant u as 用户
    participant su as 管理员
    participant a as 用户账户
    participant ha as 在线账户(热)
    participant ca as 离线账户(冷)
    participant p as 手机
    participant m as 邮箱
    participant g as Google

    u->>a: 提币
    p-->>u: 验证码
    m-->>u: 验证码
    g-->>u: 验证码
    u->>u:检验
    a-->>su: 提币通知
    su->>ha: 提币
    alt 热钱包额度不足
        ca-->>ha: 划转
        ha-->>u:提币
    else 热钱包额度充足
        ha-->>u:提币
    end
    a-->>a: 入账
    p-->>u: 通知
    m-->>u: 通知
```


## 三、属性

### 1.用户明细


| 序号 | 字段 | 备注 |
| ------ | ------ | ------ |
| 1 | 手机 |  |
| 2 | 邮箱 |  |
| 3 | Google | |
| 4 | 昵称 | |






