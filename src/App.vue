<template>
  <div id="app">
    
    <!-- :data="text"
      :footerHidden="false"
      :deleteHidden="text._id === cardId ? deleteHidden : true"
      :cancelSelected="cancelSelected"    

      :multiDelete="multiDelete"
      @getId="getId" -->
    <MultifuncCard
      :data="text1"
      :content="text1.name"
      :selectable = "true"
      :deletable = "true"
      keyword = "a"
      keywordColor = "red"
      keywordBackGround = "pink"
      :operable="true"
      :options="[
          {key: 'check', title: '查看'},
          {key: 'edit', title: '编辑'},
          {key: 'delete', title: '删除'},
      ]"
      :subscribe="-1"
      :headerable="true"
      :footerable="true"
      @select="getSelect"
      @hoverCard="hoverCard"
      @deleteSingleCard="deleteSingleCard"
      @handleMenu="handleMenu"
    >
      <div slot="header-content"  style="margin-top:2px;display: flex; align-items: center; justify-content: space-between;">
        <div>left</div>
        <div>right</div>
      </div>
      <div slot="footer-content">
        <div>{{ text1._id }}</div>
      </div>
      <!-- <template #footer-content-getData="{data}">
        <div>{{data._id}}</div>
      </template> -->
      
    </MultifuncCard>
    <MultifuncCard
      :data="text2"
      :content="text2.name"
      :selectable = "false"
      @select="getSelect"
      @hoverCard="hoverCard"
      :headerable="false"
    />
  </div>
</template>

<script>
import MultifuncCard from '../plugins/MultifuncCard/MultifuncCard.vue'

export default {
  name: 'App',
  components: {
    MultifuncCard
  },
  data() {
    return {
      text1: {
        _id: "QQQQQQ1",
        name:"I give my kids money through apps, not cash — and I'm not alone"
      },
      text2: {
        _id: "QQQQQQ2",
        name:"Generative AI Use Case Library for the Healthcare Industry"
      },
    }
  },
  methods: {
    getSelect(data){
      console.log(data);
    },
    hoverCard(status, data){
      console.log(status, data);
    },
    deleteSingleCard(data){
      console.log(data);
    },
    handleMenu (key, data) {
      console.log(key, data);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
