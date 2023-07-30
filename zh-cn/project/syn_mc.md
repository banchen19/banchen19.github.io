# MC同步器项目文档

## Http接口说明
GET请求
---
### `GET /getinformation_name`

提供玩家名字与玩家密码获取玩家信息

- 请求方式：GET
- 路径示例：/getinformation_name?name=banchen21&psw=123121
- 参数：
  - name：玩家名称
- 响应：
  - 200 OK：成功，返回玩家权限信息
    - 响应体：
    ```json
      {
    "code": 200,
    "message": {
      "data": "NULL",
      "device": "1",
      "ip": "1",
      "money": 1000,
      "name": "banchen21",
      "online": 1,
      "perm_level": 1,
      "server_name": "111",
      "xuid": "123"
      }
    }
    ```
  - 404 Not Found：资源不存在
    - 响应体：`{"code":404,"message":"null"}`
  - 403 Not Found：资源不存在
    - 响应体：`{"code":403,"message":"false"}`
---
### `GET /getinformation_xuid`

提供玩家xuid与玩家密码获取玩家信息

- 请求方式：GET
- 路径示例：：/getinformation_xuid?xuid=123&psw=123121
- 参数：
  - name：玩家名称
- 响应：
  - 200 OK：成功，返回玩家权限信息
    - 响应体：
    ```json
      {
    "code": 200,
    "message": {
      "data": "NULL",
      "device": "1",
      "ip": "1",
      "money": 1000,
      "name": "banchen21",
      "online": 1,
      "perm_level": 1,
      "server_name": "111",
      "xuid": "123"
      }
    }
    ```
  - 404 Not Found：资源不存在
    - 响应体：`{"code":404,"message":"null"}`
  - 403 Not Found：资源不存在
    - 响应体：`{"code":403,"message":"false"}`
---
### `GET /setloginpsw`

修改登录密码

- 请求方式：GET
- 路径示例：/setloginpsw?name=123&psw=123121&newpsw=123456
- 参数：
  - name：玩家名称
- 响应：
  - 200 OK：成功，返回玩家权限信息
    - 响应体：
    ```json
      {
    "code": 200,
    "message": "true"
    }
    ```
    
  - 400 Bad Request：请求格式无效。
    - 响应体：`{"code":400,"message": "false"}`
  - 403 Forbidden：客户端验证失败
    - 响应体：`{"code":403,"message":"false"}`
  - 404 Not Found：资源不存在
    - 响应体：`{"code":404,"message":"null"}`
---

### `GET /login`

检测登录

- 请求方式：GET
- 路径示例：/login?name=123&psw=123121
- 参数：
  - name：玩家名称
- 响应：
  - 200 OK：成功，返回玩家权限信息
    - 响应体：
    ```json
      {
    "code": 200,
    "message": "true"
    }
    ```
  - 404 Not Found：资源不存在
    - 响应体：`{"code":404,"message":"null"}`
  - 403 Forbidden：验证失败
    - 响应体：`{"code":403,"message":"false"}`
---
### `GET /getplayer_name`

根据玩家name检查玩家是否存在这个数据库

- 请求方式：GET
- 路径示例：/getplayer_name?name=123
- 参数：
  - name：玩家名称
- 响应：
  - 200 OK：成功，返回玩家权限信息
    - 响应体：
    ```json
      {
    "code": 200,
    "message": "true"
    }
    ```
  - 404 Not Found：资源不存在
    - 响应体：`{"code":404,"message":"null"}`

---
POST 请求
---
### `POST /post_add_player`

添加玩家白名单、添加玩家信息

- 请求方式：POST
- 路径示例：：/post_add_player
- 参数：
  - 用户数据（JSON）：
    - name：玩家名称
    - t：t 值
    - token：令牌
    - 请求头：`"Content-Type: application/json"`
- 请求体参数：
```json
{
    "key": "string",
    "v": "string",
      "player": {
    "xuid": "string",
    "name": "string",
    "psw": "string",
    "money": 0,
    "ip": "string",
    "online": 0,
    "device": "string",
    "perm_level": 0,
    "server_name": "string",
    "data": "string"
  }
}
```
- 响应：
  - 200 OK：添加成功
  ```json
    {
    "code": 200,
    "message":  "true"
    }
    ```
  - 409 Conflict：玩家已经被添加过，并且不允许继续重复添加
    - 响应体：`{"code":409,"message": "false"}`
  - 403 Forbidden：验证失败
    - 响应体：`{"code":403,"message": "false"}`

  - 400 Bad Request：客户端发送了一个错误的请求。
    - 响应体：`{"code":400,"message": "false"}`
---

### `POST /getinformation_all`

获取所有玩家信息。

- 请求方式：POST
- 路径示例：：/getinformation_all
- 参数：
  - 用户数据（JSON）：
    - name：玩家名称
    - t：t 值
    - token：令牌
    - 请求头：`"Content-Type: application/json"`
- 请求体参数：
```json
{
    "name": "banchen21",
    "token": "65f254760c19ef38a9e808478fcef633",
    "t": "1689344052555"
}
```
- 响应：
  - 200 OK：成功，返回所有玩家权限信息
  ```json
    {
    "code": 200,
    "message": {
        "players": [
            {
                "data": "NULL",
                "device": "1",
                "ip": "1",
                "money": 1000,
                "name": "banchen21",
                "online": 1,
                "perm_level": 1,
                "server_name": "111",
                "xuid": "123"
            },
            {
                "data": "NULL",
                "device": "2",
                "ip": "1",
                "money": 252,
                "name": "a",
                "online": 2,
                "perm_level": 2,
                "server_name": "222",
                "xuid": "321"
            }
        ]
    }
  }
    ```
  - 401 Unauthorized : 密钥超时
    - 响应体：`{"code":401,"message": "Unauthorized"}`
  - 403 Forbidden：验证失败
    - 响应体：`{"code":403,"message": "false"}`
  - 404 Not Found：资源不存在
    - 响应体：`{"code":404,"message": "null"}`
  - 400 Bad Request：客户端发送了一个错误的请求。
    - 响应体：`{"code":400,"message": "false"}`
---
## WS端接口说明
### Chat通信
#### 消息发送格式
```json
{
    "key":"密钥",
    "typestr":"chat",
    "data":"{
        "player_name":"玩家名",
        "perm_level":"null",
        "serverver_name":"发送这个消息的客户端",
        "data":"要广播到所有子服的消息"
    }"
}
```
#### 消息接受格式
 ```json
{
  "data":{
    "player_name":"string",
    "perm_level":0,
    "data":"chat_msg",
    "serverver_name":"玩家进行游戏服务服务端名"
  },
  "typestr":"chat",
  "serverver_name":"玩家发送消息的服务端民"
}
```
---
## 其他说明
 -POST 请求格式
 - JSON

-GET 请求格式
 - 参数
 - 示例
```
http://127.0.0.1:8082/getpermissions?name=banchen21
```