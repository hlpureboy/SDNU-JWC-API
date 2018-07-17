# 山东师范大学教务处API(学生版)

## 1.主要功能

- [x] 获取成绩
- [x] 获取个人照片
- [x] 填写教师评价
- [x] 获取个人信息
- [x] 抢课（~~公布~~）
- [ ] 获取个人课表

## 2.API使用说明

> 下列api只提供get请求访问

#### 2.1 api 列表

|   *action*   | *method* | *args* | *return* |  *content*   |
| :----------: | :------: | :----: | :------: | :----------: |
|   /getKey    |   GET    | xh,pwd |   key    |   获取key    |
|  /getScore   |   GET    |  key   |  Score   |   获取成绩   |
| /getUserInfo |   GET    |  key   | userinfo | 获取个人信息 |
|   /getPic    |   GET    |  key   |   pic    | 获取个人照片 |
|   /putVote   |   GET    |  key   |  status  | 填写教师评价 |

#### 2.2 申请key

  为了方便api的使用，避免学号，密码多次输入。通过提供key的方式进行使用。

> GET http://120.79.61.119/getKey

**GET 参数**

| 参数 | 含义       |
| ---- | ---------- |
| xh   | 学号       |
| pwd  | 教务处密码 |

**返回json数据**

| 参数   | 含义     |
| ------ | -------- |
| msg    | 状态码   |
| result | 返回结果 |

> 注意：会返回两种结果 如下

```json
{
  "msg": "105",
  "result": "出现错误"
}
{
  "msg": 100,
  "result": {
    "key": "3c2bd4abaae6d58f01ca8567e419a20e"
  }
}
```

  当出现错误时，请检查 xh，pwd是否正确，如果正确，请再次请求，因为自己训练的验证码识别可能出错
#### 2.3 获取个人信息
> GET  http://120.79.61.119/getUserInfo

| 参数 | 含义       |
| ---- | ---------- |
| key   | key值       |

> 注意同样返回两种结果
> 
```json
{
  "msg": 100,
  "reuslt": {
    "addr": "山东省xxxxxxxxxxx",
    "email": "",
    "idcard": "3707xxxxxxxx",
    "name": "彭xx",
    "phone": "",
    "sex": "x",
    "xh": "2015xxxx"
  }
}
{
  "msg": 107,
  "reuslt": "信息获取失败!"
}
```
>失败的话，请重新申请key，从而更新个人信息
>
#### 2.4 获取个人照片
>GET  http://120.79.61.119/getPic
>

| 参数 | 含义       |
| ---- | ---------- |
| key   | key值       |

> 也是返回两种结果
> 
```json
{
  "msg": 109,
  "result": "图片加载失败!"
}
失败请重新获取key
{
  "msg": 100,
  "result": {
    "content": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAwMEAwMEBQgFBQQEBQoHBwYIDAoMDAsKCwsNDhIQDQ4"
  }
}
content 中的数据是base64编码的照片
```
#### 2.5 获取个人成绩

> GET http://120.79.61.119/getScore

| 参数 | 含义       |
| ---- | ---------- |
| key   | key值       |

> 也是返回两种结果
> 
```json
{
  "msg": 106,
  "result": "获取成绩错误"
}
失败请重新，调用此接口
{
  "msg": 100,
  "result": {
    "Android平台与开发技术": "95",
    "XXXX":"xxx"
  }
}
```
#### 2.6 填写教师评价

> GET http://120.79.61.119/putVote

| 参数 | 含义       |
| ---- | ---------- |
| key   | key值       |

> 也是返回两种结果
> 
```json
{
  "msg": 108,
  "result": "评价失败"
}
失败请重新，调用此接口
{
  "msg": 100,
  "result": "提交成功!"
}
```
