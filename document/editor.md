# 编辑器

文档编辑器类，提供了获取内容、设置内容等方法。

## 构造函数

* 用法

```js
const Editor = shimo.sdk.document.Editor
const editor = new Editor({
  localeConfig: {
    fetchLocaleSync: function (locale) {
      return Editor.LocaleResources[locale]
    },
    locale: 'en-US'
  }
})
editor.render(container)
```

* 参数

| 名称               | 类型      | 默认值  | 描述             |
| ------------------ | --------- | ------- | ---------------- |
| `readOnly` | `Boolean` | `false` | 设置文档是否只读 |
| `id`| `number`      | 必选     | 用户ID     |
| `localeConfig`| `Object`      | 可选     | 国际化相关配置，如果未传，默认使用中文（zh-CN） |
| `localeConfig.locale`| `String`      | 可选     | 语言配置，`en-US`   |
| `localeConfig.fetchLocaleSync`| `Function`      | 可选     | 参数为locale，返回对应的翻译后的数据     |

## 方法列表

### render

渲染文档。

* 返回 `undefined`
* 用法 `editor.render(container, [options])`
* 参数

| 名称                | 类型          | 默认值 | 描述         |
| ------------------- | ------------- | ------ | ------------ |
| `container`         | `HTMLElement`      | 必选     | 文档渲染容器     |
| `options`         | `Options`      | 可选     | 文档渲染配置     |

* Options

| 名称                | 类型          | 默认值 | 描述         |
| ------------------- | ------------- | ------ | ------------ |
| `readOnly` | `Boolean` | `false` | 设置文档是否只读 |
| `id`| `number`      | 必选     | 用户ID     |
| `scrollingContainer`| `HTMLElement`      | 可选     | 文档滚动区     |
| `modules`| `Object`      | 可选     | 是否启用工具栏     |
| `modules.toolbar`| `Boolean / Object`      | 可选     | 是否启用工具栏     |
| `modules.toolbar.parent`| `HTMLElement`      | 可选     | 工具栏父容器     |

### updateOptions

更新配置。

* 返回 `undefined`
* 用法 `editor.updateOptions(options)`
* 参数

| 名称                | 类型          | 默认值 | 描述         |
| ------------------- | ------------- | ------ | ------------ |
| `readOnly`        | `boolean`       | 无     | 设置文档是否只读 |
| `id`| `number`      | 可选     | 用户ID     |

### getContent

获取文档内容。

* 返回 `Promise<String>`
* 用法

```js
editor.getContent().then(content => {
  console.log(content)
})
```

### setContent

设置文档内容。

* 返回 `undefined`
* 用法 `editor.setContent(content)`
* 参数

| 名称            | 类型     | 默认值 | 描述                      |
| --------------- | -------- | ------ | ------------------------- |
| `content`       | `String` | 无     | 文档内容                  |

### applyChange

给文档更新内容。

* 返回 `undefined`
* 用法 `editor.applyChange(change)`
* 参数

| 名称            | 类型     | 默认值 | 描述                      |
| --------------- | -------- | ------ | ------------------------- |
| `change`       | `String` | 无     | 修改文档的内容                  |

### getLocale

返回当前的语言环境字符串

* 返回 `string`
* 用法 `editor.getLocale()`

### destroy

销毁实例。

* 返回 `undefined`
* 用法 `editor.destroy()`

## 事件列表

* 用法

```js
const events = Editor.events
editor.on(events.CHANGE, handler)
```

### PLUGIN_LOADED

插件加载完成。

* 回调方法签名 `handler( name )`
* 参数

|名称|类型|默认值|描述|
| -- | -- | -- | -- |
| `name` | `String` | 无 | 插件名称 |

### CHANGE

当前用户产生的数据变化。

* 回调方法签名 `handler( change )`
* 参数

|名称|类型|默认值|描述|
| -- | -- | -- | -- |
| `change` | `String` | 无 | 数据 |

### SELECTION

用户的光标、选区发生变化时触发。

* 回调方法签名 `handler( range )`
* 参数

|名称|类型|默认值|描述|
| -- | -- | -- | -- |
| `range.index` | `Number` | 无 | 光标位置处于文档流中的序号 |
| `range.length` | `Number` | 无 | 选区长度（无选区就是 0） |

### READY

文件内容渲染完成。

### CONTAINER_SCROLL

编辑器滚动时触发这个事件。
