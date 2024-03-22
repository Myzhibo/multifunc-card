# multifunc-card

## Project setup
```
npm i multifunc-card
```
## functions

### Attributes
| 属性 | 描述 | 类型 | 可选值 | 默认值 | 例子
| :--: | :--: | :--: | :--: | :--: | :--: |
| selectMode | 是否开启可选模式 | Boolean | - | false | - |
| data | 卡片对象 | Object | - | - | - |
| content | 展现在卡片上的内容 | String | - | - | - |
| deletable | 卡片是否支持删除 | Boolean | - | - | - |
| keyword | 关键字高亮 | String | - | - | - |
|  | **-属性-** | **-描述-** | **-类型-** | **-默认值-** | - |
|  | - keywordColor | 高亮字体颜色 | String | white |  - |
|  | - keywordBackGround | 高亮背景色 | String | skyblue | - |
| operable | 是否开启操作表单 | Boolean | - | true | - |
|  | **-属性-** | **-描述-** | **-类型-** | **-默认值-** | - |
|  | - options | 表单内容 | Array[Object] | [] | [{key: 'edit', title: '编辑'}] |

### Slot

### Events
| 方法 | 描述 | 返回值 |
| :--: | :--: | :--: |
| select | 开启可选模式后，选择卡片时的回调 | 所选卡片的data对象 |
| getHidden | 卡片支持删除模式后，移入移出卡片时的回调 | 状态(悬停true/移出false), 所选卡片的data对象 |
| deleteSingleCard | 卡片支持删除模式后，点击删除按钮的回调 | 所选卡片的data对象 |
