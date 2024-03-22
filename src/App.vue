<template>
  <div id="app">
    
    <!-- :data="text"
      :footerHidden="false"
      :deleteHidden="text._id === cardId ? deleteHidden : true"
      :cancelSelected="cancelSelected"    
      :multiDelete="multiDelete"
      @getHidden="getHidden"
      @deleteSingleData="deleteSingleData(text._id)"
      @getId="getId"
      :subscribe = "text.subscribe"
      :unfit = "text.unfit" -->
    <MultifuncCard
      :data="text1"
      :content="text1.name"
      :selectMode = "true"
      :deletable = "true"
      keyword = "a"
      keywordColor = "red"
      keywordBackGround = "pink"
      @select="getSelect"
      @getHidden="getHidden"
      @deleteSingleCard="deleteSingleCard"
    />
    <MultifuncCard
      :data="text2"
      :content="text2.name"
      :selectMode = "true"
      @select="getSelect"
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
        name:"I give my kids money through apps, not cash — and I'm not alone"
      },
      text2: {
        name:"Generative AI Use Case Library for the Healthcare Industry"
      },
    }
  },
  methods: {
    getSelect(data){
      console.log(data);
    },
    getHidden(status, data){
      console.log(status, data);
    },
    deleteSingleCard(data){
      console.log(data);
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
