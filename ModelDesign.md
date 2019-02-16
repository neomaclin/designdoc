
##  用户
### 核心模型

```scala
final case class User(name: UserName, alias: Alias)
final case class User
```

### 持久化模型
```scala
final case class UserDetail(username: UserName,
                            email: Email,
                            password: EncryptedPassword,
                            alias: Alias)
final case class UserMemo

final case class User
```

### 通讯模型

```scala
final case class UserRegistration(
    name: UserName, 
    email: Email, 
    password: Password)

final case class Login(name: UserName, email: Email)

final case class TwoFactorLogin()

final case class ChangeRequest(changeType: ChangeType, content: String)

//
```


## 资产
### 核心模型
```scala
```

### 持久化模型
```scala
```

### 通讯模型

```scala

```


## 项目
### 核心模型
```scala
```
### 持久化模型
```scala
```
### 通讯模型
```scala
```

## 充币
### 核心模型
```scala
```

### 持久化模型
```scala
```

### 通讯模型
```scala
```

##