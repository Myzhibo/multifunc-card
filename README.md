# multifunc-card

## Project setup
```
npm i multifunc-card
```
## functions

### Attributes
| 属性 | 描述 | 类型 | 可选值 | 默认值 |
| :--: | :--: | :--: | :--: | :--: |
| selectMode | 是否开启可选模式 | Boolean | - | - |
| data | 卡片对象 | Object | - | - |
| content | 展现在卡片上的内容 | String | - | - |
| deletable | 卡片是否支持删除 | Boolean | - | - |
| keyword | 关键字高亮 | String | - | - |
|  | -属性- | -描述- | -类型- | -默认值- |
|  | - keywordColor | 高亮字体颜色 | String | white |  
|  | - keywordBackGround | 高亮背景色 | String | skyblue |


### Slot

### Events
| 方法 | 描述 |
| :--: | :--: |
| select | 开启可选模式后，选择卡片时的回调 |
| getHidden | 卡片支持删除模式，悬停卡片时的回调 |