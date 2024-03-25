# multifunc-card

## Project setup
```
npm i multifunc-card
```
## functions

### Attributes
| 属性 | 描述 | 类型 | 可选值 | 默认值 | 例子
| :--: | :--: | :--: | :--: | :--: | :--: |
| shadow | 设置阴影显示时机 | string | always / hover / never | always | - |
| selectable | 是否开启可选模式 | Boolean | - | false | - |
| data | 卡片对象 | Object | - | - | - |
| content | 展现在卡片上的内容 | String | - | - | - |
| headerable | 是否开启头部内容区 | Boolean | - | true | - |
| footerable | 是否开启底部内容区 | Boolean | - | true | - |
| deletable | 是否支持删除 | Boolean | - | false | - |
| keyword | 关键字高亮 | String | - | - | - |
| subscribe | 订阅 | Number | -1(红色底色) 0(无底色) 1(绿色底色)| 0 | - |
|  | **-属性-** | **-描述-** | **-类型-** | **-默认值-** | - |
|  | - keywordColor | 高亮字体颜色 | String | white |  - |
|  | - keywordBackGround | 高亮背景色 | String | skyblue | - |
| operable | 是否开启尾部操作表单 | Boolean | - | true | - |
|  | **-属性-** | **-描述-** | **-类型-** | **-默认值-** | - |
|  | - options | 表单内容 | Array[Object] | [] | [{key: 'edit', title: '编辑'}] |

### Slot
| slot名 | 类型 | 描述 |
| :--: | :--: | :--: |
| header-content | 具名插槽 | 开启头部内容区后，可向卡片顶部放置内容的插槽 | 
| footer-content | 具名插槽 | 开启底部内容区后，可向卡片底部放置内容的插槽 | 

### Events
| 方法 | 描述 | 回调参数 |
| :--: | :--: | :--: |
| hoverCard | 移入移出卡片时的回调 | 状态(悬停true/移出false), 悬停卡片的data对象 |
| select | 点击卡片的回调 / 开启可选模式后，选择卡片时的回调 | 所选卡片的data对象 |
| deleteSingleCard | 卡片支持删除模式后，点击删除按钮的回调 | 所选卡片的data对象 |
| handleMenu | 卡片开启尾部操作表单后，点击菜单选项时的回调 | key, 所选卡片的data对象 |
