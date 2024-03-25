<template>
  <div>
    <div
      slot="signal"
      class="text-card-container"
      style="position: relative; margin-bottom: 10px"
      :class="{ 'select-mode': selectable }"
    >
      <!-- 是否可选模式 -->
      <el-checkbox v-if="selectable" v-model="data.checked" style="margin-right: 10px;" @change="getBeChecked" />
      <!-- 卡片 -->
      <el-card
        ref="elCard"
        v-bind="this.$attrs"

        style="width: 100%"
        @mouseenter.native="hoverCard"
        @mouseleave.native="leaveCard"
        @click.native="handleCardClick"
        :class="[
          // data.inBasket ? 'in-basket' : '',
          subscribe === 1 ? 'subscribe' : (subscribe === -1 ? 'unSubscribe' : ''),
        ]"
      >
          <!-- 继承ui组件本身的插槽 -->
          <template v-for="(value, name) in $slots" #[name]="scopedData">
            <slot :name="name" v-bind="scopedData"></slot>
          </template>
          <!-- 删除文章篮图标显隐 -->
          <div
            v-if="deletable && ishoverCard"
            class="text-card-container-left"
            style="position: absolute; top: 0px; right: 0px; cursor: pointer"
          >
            <i
              class="el-icon-error deleteIcon"
              style="color: rgba(171, 50, 50, 0.822) ; font-size: 23px"
              @click.stop="deleteSingleCard" />
          </div>
          <!-- 批量删除文章篮图标显隐 -->
          <div
            v-show="multiDelete"
            :class="{ active: isActive }"
            style="position: absolute; top: 0px; right: 0px; cursor: pointer"
          >
            <i class="el-icon-error deleteIcon" style="font-size: 23px" />
          </div>
          <!-- header -->
          <div v-if="headerable" class="text-card-container-header" >
            <slot name="header-content"></slot>
          </div>
          <!-- 正文内容 -->
          <div style="display: flex; align-items: center; justify-content: center; position:relative">
              <div v-html="highlight( content )" style="width:90%" />
              <div v-if="operable" class="c-readingset-item-inner-ops" style="position:absolute; right:-15px;">
                <el-dropdown @click.native.stop @command="handleCommand($event, data)">
                  <span class="el-dropdown-link">
                    <el-link :underline="false"> <i class="el-icon-more" style="font-size: 20px" /> </el-link>
                  </span>
                  <el-dropdown-menu slot="dropdown">
                    <el-dropdown-item :command="op.key" :key="op.key" v-for="op of options">
                      {{op.title}}
                    </el-dropdown-item>
                  </el-dropdown-menu>
                </el-dropdown>
              </div>
          </div>
          <!-- footer -->
          <div class="footer" v-if="footerable">
            <!-- 为父组件放置一个插槽 -->
            <slot name="footer-content"></slot>    <!-- 具名插槽： 只放置插槽、用来[接收]父组件传值 -->
            <!-- <slot name="footer-content-getData" :data="data"></slot>     放置一个作用域插槽并[向]父组件传值 -->
          </div>
      </el-card>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CP_MyCard',
  data(){
    return {
      ishoverCard: false,

      isActive: false,
    }
  },
  props: {
    // 是否开启可选模式
    selectable: {
      type: Boolean,
      default: false,     
    },
    // 卡片对象
    data: Object,
    // 卡片内容
    content: String,
    // 是否开启卡片头部
    headerable: {
      type: Boolean,
      default: true,    
    },
    // 是否开启卡片底部
    footerable: {
      type: Boolean,
      default: true,    
    },
    // 高亮关键词
    keyword: String,
    // 高亮关键词 字体颜色
    keywordColor: {
      type: String,
      default: 'white',
    },
    // 高亮关键词 背景颜色
    keywordBackGround: {
      type: String,
      default: 'skyblue',
    },
    // 是否支持删除
    deletable: {
      type: Boolean,
      default: false,
    },
    // 是否开启操作表单
    operable: {        
      type: Boolean,
      default: false,
    },
    // 表单内容
    options: {        
      type: Array,
      default: () => [],
    },
    // 订阅
    subscribe: {    
      type: Number,
      default: 0,
    },



    open: {
      type: Boolean,
      default: false,      // 开启过渡动画
    },
    multiDelete: {
      type: Boolean,
      default: false,   // 是否开启批量删除模式
    },
    cancelSelected: {
      type: Boolean,
      default: false,   // 是否取消批量删除选中的卡片
    },
  },
  components: {
  },
  mounted(){
    // const elCard = this.$refs.elCard;
    // for (const key in elCard) {
    //   this[key] = elCard[key];
    // }
  },
  watch: {
    cancelSelected() {
      if (this.cancelSelected === false) {
        this.isActive = false;
      } else {
        this.isActive = true;
      }
    }
  },
  methods:{
    // 关键字高亮
    highlight(html) {
      if (!this.keyword) {
        return html;
      }
      if (html) {
        return html.replace(new RegExp(this.keyword, 'gi'), (...args) => {
          // return `<span class="highlight" :style="{ 'color': '${this.keywordColor}', 'backgroundColor': '${this.keywordBackGround}' }" >${args[0]}</span>`;
          return `<span class="highlight" style="color:${this.keywordColor}; background-color:${this.keywordBackGround}; }" >${args[0]}</span>`;
        });
      }
    },
    // 可选模式下，选中多选框通知父组件触发'select'
    getBeChecked() {
      this.data.checked = !this.data.checked;
      this.$set(this.data, 'checked', !this.data.checked);
      this.$emit('select', this.data);
    },
    // 鼠标移入卡片
    hoverCard() {
      this.ishoverCard = true;
      this.$emit('hoverCard', this.ishoverCard, this.data);
    },
    // 鼠标移出卡片
    leaveCard() {
      this.ishoverCard = false;
      this.$emit('hoverCard', this.ishoverCard, this.data);
    },
    // 删除卡片
    deleteSingleCard() {
      this.$emit('deleteSingleCard', this.data)
    },
    // 鼠标点击卡片
    handleCardClick() {
      if (this.selectable) {
        this.$set(this.data, 'checked', !this.data.checked);
        this.$emit('select', this.data);
        return;
      }
      if (this.multiDelete) {
        return this.clickDelete();
      }
      this.$emit('select', this.data);
    },
    // 操作
    handleCommand(key, item) {
      // this.book = item;
      this.$emit('handleMenu', key, item);
    }
    
  },

}
</script>

<style scoped lang="scss">
.active {
  color: rgba(190, 32, 32, 1);
}
// 设置文字自适应
.dynamic_font2 {
  white-space: nowrap; /*文字不换行*/
  overflow: hidden; /*超出部分隐藏*/
  text-overflow: ellipsis; /*溢出部分用省略号表示*/
}
@media screen and (max-width: 1005px) {
  .dynamic_font2 {
    font-size: 2px;
    width: 60px;
  }
}
@media screen and (max-width: 950px) {
  .dynamic_font2 {
    font-size: 2px;
    width: 30px;
  }
}
.text-card-container {
  width: 100%;
  cursor: pointer;
  &.select-mode {
    display: flex;
    align-items: center;
  }
  &-header {
    .c-full-pipeline {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      align-items: flex-end;
    }
    .c-full-pipeline-info {
      display: flex;
      flex-wrap: nowrap;
      > a {
        cursor: pointer;
        text-decoration: underline;
        white-space: nowrap;
        &:not(:last-child) {
          margin-right: 5px;
        }
      }
      a:hover{
        color: rgb(0, 68, 255);
      }
    }
  }
  &-content {
    width: 100%;
    .title {
      margin-bottom: 0px;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    .abstract,
    .origin_article {
      max-height: 60px;
      overflow: hidden;
      text-overflow: ellipsis;
    }
  }
  &-footer {
    width: 100%;
  }
}
.in-basket {
  background-color: rgb(233, 253, 233);
}

.subscribe {
  background-color: rgb(233, 253, 233);
}

.unSubscribe {
  background-color: rgb(253, 233, 233);
}

.disabled {
  pointer-events: none;
}

::v-deep .el-card {
  border-color: #ddd;
  border-radius: 5px;

  // .highlight {
  //   background-color: skyblue;
  //   color: white;
  // }
}
::v-deep .el-card__body {
  padding: 10px 20px;
}

.footer{
  // display: flex;
  // align-items: center;
  // justify-content: space-between; 
  
  border-top: 1px solid rgba(0, 0, 0, 0.1);
  padding-top: 10px;
}

.c-readingset-item {
  cursor: pointer;
  margin-bottom: 10px;
  margin-right: 5px;
  box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.13);
  &-inner {
    display: flex;
    &-icon {
      position: relative;
      top: 20px;
      left: -5px;
      flex: none;
    }
    &-content {
      flex: auto;
      width: calc(100% - 90px);
      &-title {
        font-size: 20px;
        font-weight: 20px;
        margin-bottom: 3px;
        // background-color: red;
      }
      &-guide {
        font-size: 14px;
        font-weight: 14px;
        width: 95%;
        margin-bottom: 5px;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        // background-color: green;
      }
      &-info {
        display: flex;
        font-size: 12px;
        // background-color: yellow;
        > span {
          padding: 3px 0px;
          color: #666;
          display: flex;
          align-items: center;
          justify-content: center;
        }
      }
    }
    &-ops {
      flex: none;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-right: 10px;
    }
  }
}
::v-deep .deleteIcon:hover {
  color: rgba(190, 32, 32, 1) !important;
}
</style>