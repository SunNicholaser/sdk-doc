# 文档mention插件

加载此插件可以使得编辑器支持@人与文件。

## 构造函数

* 用法

```js
const Editor = shimo.sdk.document.Editor
const Mention = shimo.sdk.document.plugins.Mention
const editor = new Editor()
const mention = new Mention({
  editor,
  ...options
})
```

* 参数

|名称|类型|默认值|描述|
| -- | -- | -- | -- |
| `editor` | `Editor` | 必选 | 编辑器实例 |
| `id` | `string` | 可选 | 容器id |
| `scrollContainer` | `Element` | 可选 | 滚动容器 |
| `service` | `Service` | 必选 | 接口配置 |
| `user` | `User` | 必选 | 用户信息 |
| `file` | `File` | 必选 | 文件信息 |

* Service

|名称|类型|默认值|描述|
| -- | -- | -- | -- |
| `recentContacts` | `string` | 必选 | 最近联系人 |
| `recentFiles` | `string` | 必选 | 最近使用文件 |
| `searchApi` | `string` | 必选 | 搜索接口 |

* User

| 名称                | 类型             | 描述                |
| ------------------- | --------------- | ------------------ |
| `id`         | `Number`   |  用户ID   |
| `teamId`         | `Number`   |  用户组ID    |

* File

| 名称                | 类型             | 描述                |
| ------------------- | --------------- | ------------------ |
| `id`         | `Number`   |  文件ID   |
| `guid`         | `String`   |  文件GUID    |
| `teamId`         | `Number`   |  文件所属用户组ID    |


## 方法列表

## destroy

销毁实例。

* 返回 `undefined`
* 用法 `mention.destroy()`

## 事件列表

```js
// 搜索前
mention.on(Mention.events.SEARCHBEFORE, () => {})
// 搜索后
mention.on(Mention.events.SEARCHAFTER, () => {})
// 确认
mention.on(Mention.events.COMPLETED, (data: {
  type: 'user' | 'file',
  data: User | File
}) => {})
// 下拉框显示
mention.on(Mention.events.SHOW, () => {})
// 下拉框隐藏
mention.on(Mention.events.HIDE, () => {})
```

## 依赖后台接口说明

| 接口                | 描述                |
| ------------------- | ------------------ |
| recentContacts                | 返回用户最近联系人列表               |
| recentFiles                | 返回用户最近使用文件列表                |
| searchApi                | 返回搜索结果                |

### recentContacts

* type: `GET`
* 参数: 无
* 返回值

| 名称                | 类型             | 描述                |
| ------------------- | --------------- | ------------------ |
| `code`         | `Number`   |  错误编码，正常为0    |
| `data`         | `User[]`   |  接口实际返回值, 用户列表    |

* User

| 名称                | 类型             | 描述                |
| ------------------- | --------------- | ------------------ |
| `id`         | `Number`   |  用户ID   |
| `name`         | `String`   |  用户名    |
| `avatar`         | `String`   |  用户头像    |
| `email`         | `String`   |  用户邮箱    |
| `teamId`         | `Number`   |  用户组ID    |
| `teamRole`         | `String`   |  用户组角色   |

* 返回值示例

``` JSON
{
  "code": 0,
  "data": [
    {
      "avatar": "string",
      "email": "string",
      "id": 0,
      "name": "string",
      "teamId": 0,
      "teamRole": "member"
    }
  ]
}
```

### recentFiles

* type: `GET`
* 参数: 无
* 返回值

| 名称                | 类型             | 描述                |
| ------------------- | --------------- | ------------------ |
| `code`         | `Number`   |  错误编码，正常为0    |
| `data`         | `object`   |  接口实际返回值    |
| `data`         | `File[]`   |  最近使用文件列表    |

* File

| 名称                | 类型             | 描述                |
| ------------------- | --------------- | ------------------ |
| `id`         | `Number`   |  文件ID   |
| `name`         | `String`   |  文件名    |
| `type`         | `String`   |  文件类型 `folder, docs, sheet, slide`    |
| `guid`         | `String`   |  文件GUID    |
| `updated_at`         | `Date`   |  文件更新时间    |

* 返回值示例

``` JSON
{
  "code": 0,
  "data": [
    {
      "id": 0,
      "guid": "string",
      "name": "string",
      "type": "string",
      "updated_at": "2018-08-20T12:56:14.519Z"
    }
  ]
}
```

### searchApi

* type: `POST`
* 参数

| 名称                | 类型             | 默认值 | 描述                |
| ------------------- | --------------- | ----- | ------------------ |
| `keyword`         | `String`   | 无     | 关键词     |
| `fileId`         | `Number`   | 无     | 文件ID     |
| `teamId`         | `Number`   | 无     | 用户组ID     |
| `page`         | `Number`   | 无     | 分页页码     |
| `pageSize`         | `Number`   | 无     | 分页大小     |

* 返回值

| 名称                | 类型             | 描述                |
| ------------------- | --------------- | ------------------ |
| `code`         | `Number`   |  错误编码，正常为0    |
| `data`         | `object`   |  接口实际返回值    |
| `data.recent_contact.results`         | `User[]`   |  最近联系人搜索结果    |
| `data.team_member.results`         | `User[]`   |  用户所在组搜索结果    |
| `data.collaborator.results`         | `User[]`   |  当前文件协作者搜索结果    |
| `data.file_name.results`         | `FileObject[]`   |  文件名搜索结果    |

* User

| 名称                | 类型             | 描述                |
| ------------------- | --------------- | ------------------ |
| `id`         | `Number`   |  用户ID   |
| `name`         | `String`   |  用户名    |
| `avatar`         | `String`   |  用户头像    |
| `email`         | `String`   |  用户邮箱    |
| `teamId`         | `Number`   |  用户组ID    |
| `teamRole`         | `String`   |  用户组角色   |

* File

| 名称                | 类型             | 描述                |
| ------------------- | --------------- | ------------------ |
| `id`         | `Number`   |  文件ID   |
| `name`         | `String`   |  文件名    |
| `type`         | `String`   |  文件类型 `folder, docs, sheet, slide`    |
| `guid`         | `String`   |  文件GUID    |
| `updated_at`         | `Date`   |  文件更新时间    |

* FileObject

| 名称                | 类型             | 描述                |
| ------------------- | --------------- | ------------------ |
| `source`         | `File`   |  文件信息   |


* 返回值示例

``` JSON
{
  "code": 0,
  "data": {
    "recent_contact": {
      "count": 0,
      "page": 0,
      "pageCount": 0,
      "results": [
        {
          "avatar": "string",
          "email": "string",
          "id": 0,
          "name": "string",
          "teamId": 0,
          "teamRole": "member"
        }
      ]
    },
    "team_member": {
      "count": 0,
      "page": 0,
      "pageCount": 0,
      "results": [
        {
          "avatar": "string",
          "email": "string",
          "id": 0,
          "name": "string",
          "teamId": 0,
          "teamRole": "member"
        }
      ]
    },
    "collaborator": {
      "count": 0,
      "page": 0,
      "pageCount": 0,
      "results": [
        {
          "avatar": "string",
          "email": "string",
          "id": 0,
          "name": "string",
          "teamId": 0,
          "teamRole": "member"
        }
      ]
    },
    "file_name": {
      "count": 0,
      "page": 0,
      "pageCount": 0,
      "results": [
        {
          source: {
            "id": 0,
            "guid": "string",
            "name": "string",
            "type": "string",
            "updated_at": "2018-08-20T13:10:39.847Z"
          }
        }
      ]
    }
  }
}
```