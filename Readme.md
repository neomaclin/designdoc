# 源铸产品设计

## 产品概况
源铸平台是基于Jetmint[1]实现的去中心化投融平台，平台规范了项目方的代币发行，项目募集的流程，降低项目方跑路风险，保障代投机构、投资个体的资产安全，同时平台整合了ICO模式下的业务场景，实现了代币完整生命周期管理，包括代币的发行、募集、分发、回收、销毁以及二级市场的流通。

## 产品目标
1.利用Jetmint网络，实现全球投融项目的

## 解决的问题


## 一、模块划分

源铸社区组织结构
```mermaid
graph TB
源铸社区 --> 用户
用户 --> 账户
源铸社区 --> 项目
账户 -.-> 项目
账户 --> 资产
源铸社区 --> 媒体
源铸社区 --> 推广
源铸社区 --> 活动
活动 --> 矿池
源铸社区 --> 其他
```

源铸媒体组织结构
```mermaid
graph TB

媒体 --> 微信
媒体 --> QQ
媒体 --> Telegrem
媒体 --> Twitter
媒体 --> Facebook
媒体 --> 公众号
```

源铸其他组织结构
```mermaid
graph TB

其他 --> 公告
其他 --> 关于
其他 --> 资费说明
其他 --> FAQ
其他 --> 风险提示
其他 --> 加入我们
```

源铸推广组织结构
```mermaid
graph TB

推广 --> 新浪微博
推广 --> QQ空间
推广 --> 豆瓣
推广 --> QQ
推广 --> 微信
```

源铸用户组织结构
```mermaid
graph TB

用户 --> 用户注册
用户注册 --> 密码找回
用户 --> 用户明细
用户 --> 检验机制
用户 --> 通知机制
通知机制 --> 手机
通知机制 --> 邮件
检验机制 --> 邮件
检验机制 --> 手机
检验机制 --> Google
检验机制 --> keybase
用户 --> 账户
用户 --> 项目
```

源铸账户组织结构
```mermaid
graph TB

账户 --> 链下账户
账户 --> 链上账户
链下账户 --> 用户账户
用户账户 --> 账户明细
用户账户 --> 项目
链下账户 --> 管理员账户
管理员账户 --> 网络手续费账户
管理员账户 --> 募集手续费账户
管理员账户 --> 资产发行佣金账户
管理员账户 --> 呆坏账账户
链上账户 --> 热账户
链上账户 --> 冷账户
链上账户 --> 资产发行账户
链上账户 --> 提币账户
热账户 --> stellar
冷账户 --> stellar
资产发行账户 --> stellar
提币账户 --> stellar
```

源铸资产组织结构
```mermaid
graph TB

资产 --> 可用资产
资产 --> 冻结资产 
资产 --> 资产明细
冻结资产 --> 冻结明细
冻结明细 --> 提币冻结明细
冻结明细 --> 项目冻结明细
冻结明细 --> 参与冻结明细
资产 --> 充值明细
资产 --> 提取明细
```

源铸项目组织结构
```mermaid
graph TB

项目 --> 募集项目
募集项目 --> 项目明细
募集项目 --> 白名单
项目 --> 空投项目
空投项目 --> 项目明细
项目 --> 置换项目
置换项目 --> 项目明细
置换项目 --> 白名单
项目 --> 回收项目
回收项目 --> 项目明细
回收项目 --> 白名单

```

角色
```mermaid
graph TB

id1-0((用户)) --> id1-1((项目方))
id1-0((用户)) --> id1-2((参投方))

id2((管理员))
```


## 二、业务场景案例

### 1. 用户相关流程

流程案例：用户登记
```mermaid

sequenceDiagram
    participant u as 用户
    participant r as 注册
    participant a as 账户
    participant c as 检验机制
    participant n as 通知机制
    

    u ->> r: 注册
    r ->> c: 生成结果
    c ->>u: 验证码检验
    u ->u: 密码登记
    u -->>a: 登记默认账户
    n -->>u: 结果
    Note right of a: 普通账户类型

```

流程案例：用户密码重置
```mermaid

sequenceDiagram
    participant u as 用户
    participant r as 注册
    participant c as 检验机制
    participant n as 通知机制

    u ->> r: 请求重置
    r -->> c: 生成结果
    c ->>u: 验证码检验
    u ->>u: 密码重置
    n -->>u: 结果

```

流程案例：用户冻结
```mermaid

sequenceDiagram
    participant s as 管理员
    participant u as 用户
    participant a as 账户
    participant ai as 账户接口
    participant n as 通知机制

    s->>u: 解冻
    u->>u: 指定账户或默认全部账户
    u-->> ai: 解冻
    ai-->>a: 生成结果
    a-->> n: 操作结果
    a-->> a: 解冻
    n-->>u: 结果
```

流程案例：用户解冻
```mermaid

sequenceDiagram
    participant s as 管理员
    participant u as 用户
    participant a as 账户
    participant ai as 账户接口
    participant n as 通知机制

    s->>u: 冻结
    u->>u: 指定账户或默认全部账户
    u-->> ai: 冻结
    ai-->>a: 生成结果
    a-->> n: 操作结果
    a-->> a: 冻结
    n-->>u: 结果


```

流程案例：用户检验信息解绑
```mermaid

sequenceDiagram
    participant s as 管理员
    participant u as 用户
    participant c as 检验机制
    participant n as 通知机制

    s->>u: 选择解绑方式
    u-->>c: 解绑
    c-->>n: 操作结果
    n-->>u: 结果
    
```

### 2. 资产管理

流程案例：源铸资产账户
```mermaid

sequenceDiagram
    participant su as 管理员
    participant ai as 账户接口
    participant ha as 热账户
    participant ca as 冷账户

    su-->>ai: 创建账户
    ai-->>ha: 生成
    ha->>ai: 添加多签
    ai-->>ha: 生成结果
    ai-->>ca: 生成
    ca->>ai: 添加多签
    ai-->>ca: 生成结果

    loop 每日10:00AM
        alt 热账户大于总额度1%
            ha -->> su: 划转通知
            su ->> ai: 多签检验(threshold=2)
            ai -->> ha: 生成结果
            ha -->> ca: 划转
        else 冷账户大于总额度99%
            ca -->> su: 划转通知
            su ->> ai: 多签检验(threshold=6)
            ai-->> ca: 生成结果
            ca -->> ha: 划转
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
    participant n as 通知机制
    u->>s: 发行资产
    s-->>ca: 发行
    ca-->>na: 划转
    ca-->>ca: 账户权限死锁
    a-->>a: 90%资产入账
    Note right of a:10%资产作为发行<br>佣金
    a-->> n: 操作结果
    n-->>u: 通知
```

流程案例：充值
```mermaid

sequenceDiagram
    participant u as 用户
    participant a as 用户账户
    participant ha as 在线账户(热)
    participant n as 通知机制
    u->>a: 充值
    ha-->>ha: 到账检验
    ha-->>a: 余额映射
    ha-->> n: 操作结果
    n-->>u: 通知
```

流程案例：提币
```mermaid

sequenceDiagram
    participant u as 用户
    participant su as 管理员
    participant a as 用户账户
    participant ha as 在线账户(热)
    participant ca as 离线账户(冷)
    participant n as 通知机制
    participant c as 检验机制

    u->>a: 提币
    n-->>u: 验证码
    c-->>u: 验证码
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
    n-->>u: 通知
```

### 3. 项目管理

流程案例：募集项目管理
```mermaid

sequenceDiagram
    participant u1 as 项目方
    participant a1 as 用户账户(项目方)
    participant a3 as 用户账户(jetmint矿石)
    participant pr as 项目
    participant u2 as 参投方
    participant a2 as 用户账户(参投方)
    participant n as 通知机制
    participant g as Google

    u1->>pr: 发起募集
    a1->>pr: 缴纳手续费
    note right of a1:募集额度1%手续费
    pr-->>a1: 配额冻结
    n-->>u2: 验证码
    g-->>u2: 验证码
    u2->>u2: 检验
    u2->>pr: 参与募集
    pr-->>a2: 参与额冻结
    n-->>u2: 通知
    opt 项目到期或参与额度已满
        u1->>pr: 分发
        pr-->>a1: 解除冻结
        a1-->>a1: 结算入账
        pr-->>a2: 解除冻结
        a2-->>a2: 结算入账
        n-->>u2: 通知
        opt jetmint挖矿活动周期内
            a3-->>a1: 挖矿奖励
            note right of a1:缴纳手续费的80%<br>兑换为XYZ作为奖励 
            a1-->>a1:入账
            n-->>u1: 通知
        end
    end
    opt 项目方取消项目
        n-->>u1: 验证码
        g-->>u1: 验证码
        u1->>u1: 检验
        u1->>pr: 取消
        pr-->>a1: 解除冻结
        a1-->>a1: 结算入账
        pr-->>a2: 解除冻结
        a2-->>a2: 结算入账
        n-->>u2: 通知
        opt jetmint挖矿活动周期内
            a3-->>a1: 50%挖矿奖励
            note right of a1:缴纳手续费的80%<br>兑换为XYZ作为奖励 
            a1-->>a1:入账
            n-->>u1: 通知
            opt 有参与方
                a3-->>a2: 30%挖矿奖励
                note right of a2:按照参与方参与额度比例奖励 
                a2-->>a2:入账
                n-->>u2: 通知
            end
        end
    end

```

流程案例：置换项目管理
```mermaid
    sequenceDiagram
    participant u1 as 项目方
    participant a1 as 用户账户(项目方)
    participant pr as 项目
    participant u2 as 参投方
    participant a2 as 用户账户(参与方)
    participant n as 通知机制
    participant g as Google

    n-->>u1: 验证码
    g-->>u1: 验证码
    u1->>u1: 检验
    u1->>pr: 发起置换
        note right of pr:支持多币种置换<br>多币种
    pr-->>a1: 配额冻结
    n-->>u2: 验证码
    g-->>u2: 验证码
    u2->>u2: 检验
    u2->>pr: 参与置换
    a1-->>a1: 结算入账
    a2-->>a2: 结算入账
    n-->>u2: 通知
    opt 项目方取消项目
        n-->>u1: 验证码
        g-->>u1: 验证码
        u1->>u1: 检验
        u1->>pr: 取消
        pr-->>a1: 解除冻结
        a1-->>a1: 结算入账
    end
```

流程案例：回收项目管理
```mermaid
    sequenceDiagram
    participant u1 as 项目方
    participant a1 as 用户账户(项目方)
    participant pr as 项目
    participant u2 as 参投方
    participant a2 as 用户账户(参与方)
    participant n as 通知机制
    participant g as Google

    n-->>u1: 验证码
    g-->>u1: 验证码
    u1->>u1: 检验
    u1->>pr: 发起回收
        note right of pr:支持多币种回收<br>多币种,回收资产<br>进行销毁
    pr-->>a1: 配额冻结
    n->>u2: 验证码
    g-->>u2: 验证码
    u2->>u2: 检验
    u2->>pr: 参与回收
    a1-->>a1: 结算入账
    pr-->>pr: 创建黑洞账户，销毁
    a2-->>a2: 结算入账
    n-->>u2: 通知
    
    opt 项目方取消项目
        n-->>u1: 验证码
        g-->>u1: 验证码
        u1->>u1: 检验
        u1->>pr: 取消
        pr-->>a1: 解除冻结
        a1-->>a1: 结算入账
    end
```

流程案例：空投项目管理
```mermaid
    sequenceDiagram
    participant u1 as 项目方
    participant a1 as 用户账户(项目方)
    participant pr as 项目
    participant u2 as 参投方
    participant a2 as 用户账户(参与方)
    participant n as 通知机制
    participant g as Google

    opt 高级空投
        u1->>pr: 发起调研
        pr->>u1: 调研报告
        n-->>u1: 通知
    end 
    n-->>u1: 验证码
    g-->>u1: 验证码
    u1->>u1: 检验
    u1->>pr: 发起空投
    pr-->>a1: 配额冻结
    u2->>pr: 领取资格检验
    opt 资格有效
        u2->>a2: 地址认证及绑定
        u2->>pr: 领取空投
        a2-->>a2: 结算入账
        n-->>u2: 通知
    end
    opt 空投周期结束
        pr-->>a1: 解除冻结
        a1-->>a1: 结算入账
        n-->>u1: 通知
    end
```