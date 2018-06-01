# 历史

## 获取历史列表

**接口**

`GET <SHIMO_API>/files/:guid/histories`

**参数说明**

| 参数      | 类型   | 必填 | 说明 |
| :------- | :----- | :-- | :-- |
| size | Number | N   | 返回的历史条数，默认 `10` |
| from | Number | N   | 从第几条历史开始查找，默认 `0` |

**代码示例**

{% tabs nodeDemo="Node.js" %}

{% content "nodeDemo" %}

```js
const request = require('node-fetch')

fetch('<SHIMO_API>/files/JyRX1679PL86rbTk/histories', {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer 716570ab11db4b349051e570ac2dff13'
  }
})
  .then(res => res.json())
  .then(body => console.log(body.data))
```

{% endtabs %}

**返回示例**

```json
{
  "data": {
    "guid": "JyRX1679PL86rbTk",
    "type": "document",
    "histories": [{
      "fileGuid": "JyRX1679PL86rbTk",
      "historyType": 1,
      "userId": "10676",
      "updatedAt": "2018-05-29T09:07:51.000Z",
      "createdAt": "2018-05-29T09:07:51.000Z",
      "id": 434594,
      "content": "{\"action\":\"create\"}"
    }],
    "isLastPage": false,
    "limit": null
  },
  "code": 0
}
```

## 获取历史

**接口**

`GET <SHIMO_API>/files/:guid/histories/:id`

**代码示例**

{% tabs nodeDemo="Node.js" %}

{% content "nodeDemo" %}

```js
const request = require('node-fetch')

fetch('<SHIMO_API>/files/JyRX1679PL86rbTk/histories/434594', {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer 716570ab11db4b349051e570ac2dff13'
  }
})
  .then(res => res.json())
  .then(body => console.log(body.data))
```

{% endtabs %}

**返回示例**

```json
{
  "data": {
    "fileGuid": "JyRX1679PL86rbTk",
    "historyType": 1,
    "userId": "10676",
    "updatedAt": "2018-05-29T09:07:51.000Z",
    "createdAt": "2018-05-29T09:07:51.000Z",
    "id": 434594,
    "content": "{\"action\":\"create\"}"
  },
  "code": 0
}
```

## 创建历史

**接口**

`POST <SHIMO_API>/files/:guid/histories`

**参数说明**

| 参数      | 类型   | 必填 | 说明 |
| :------- | :----- | :-- | :-- |
| content | String | Y   | 历史内容 |
| historyType | Number | Y   | 历史类型<br>`1`：和文档**信息**有关的改动，如创建、重命名、分享<br>`2`：和文档**内容**有关的改动，如内容更改 |

**代码示例**

{% tabs nodeDemo="Node.js" %}

{% content "nodeDemo" %}

```js
const request = require('node-fetch')

fetch('<SHIMO_API>/files/JyRX1679PL86rbTk/histories', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer 716570ab11db4b349051e570ac2dff13'
  },
  body: JSON.stringify({
    thistoryTypeype: 1,
    content: '{\"action\":\"create\"}'
  })
})
  .then(res => res.json())
  .then(body => console.log(body.data))
```

{% endtabs %}

**返回示例**

```json
{
  "data": {
    "fileGuid": "JyRX1679PL86rbTk",
    "historyType": 1,
    "userId": "10676",
    "updatedAt": "2018-05-29T09:07:51.000Z",
    "createdAt": "2018-05-29T09:07:51.000Z",
    "id": 434594,
    "content": "{\"action\":\"create\"}"
  },
  "code": 0
}
```

## 获取指定历史的文档名

**接口**

`GET <SHIMO_API>/files/:guid/histories/:id/title`

**代码示例**

{% tabs nodeDemo="Node.js" %}

{% content "nodeDemo" %}

```js
const request = require('node-fetch')

fetch('<SHIMO_API>/files/JyRX1679PL86rbTk/histories/434594', {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer 716570ab11db4b349051e570ac2dff13'
  }
})
  .then(res => res.json())
  .then(body => console.log(body.data))
```

{% endtabs %}

**返回示例**

```json
{
  "data": "无标题",
  "code": 0
}
```