<template>
  <div id="app">
    <Header />
    <div class="entry">
      LOREM IPSUM
      <b>DOLOR SIT AMET</b>
    </div>
    <div class="content">
      <List
        v-for="data in dataGroup"
        :key="data.id"
        :listdata="data"
      />
    </div>
  </div>
</template>

<script>
import Header from '@/components/Header'
import List from '@/components/List'

export default {
  components: {
    Header,
    List
  },
  data () {
    return {
      dataGroup: [],
      favories: []
    }
  },
  created () {
    fetch('https://dtv-projects.firebaseio.com/sections.json')
      .then((res) => { return res.json() })
      .then((res) => {
        this.dataGroup = res
      })
  }
}
</script>

<style lang="less">
@import  './assets/less/variables.less';

body {
  background: #232530 url('./assets/images/header.png') no-repeat top center;
  background-size: contain;
  color: #fff;
  margin: 0;
  padding: 50px 0 0;
}
* {
  box-sizing: border-box;
}
a {
  color: #fff;
  text-decoration: none;
}
#app {
  font-family: 'Open Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 1160px;
  padding: 0 20px;
  margin: auto;
}
.entry {
  text-align: center;
  font-size: 40px;
  padding: 400px 0 100px;
  b {
    display: block;
  }
  @media @tablet {
    padding: 200px 0 50px
  }
}
</style>
