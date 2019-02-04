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
      <Favorites
        v-if="favorites.length > 2"
        :favoritesdata="favorites"
      />
    </div>
  </div>
</template>

<script>
import Header from '@/components/Header'
import List from '@/components/List'
import Favorites from '@/components/Favorites'
import { eventBus } from './main'

export default {
  components: {
    Header,
    List,
    Favorites
  },
  data () {
    return {
      dataGroup: [],
      favorites: []
    }
  },
  methods: {
    addFavorites (fItem) {
      this.favorites.push(fItem)
      localStorage.setItem('favories', JSON.stringify(this.favorites))
    },
    removeFavorites (i) {
      this.$delete(this.favorites, i)
      localStorage.setItem('favories', JSON.stringify(this.favorites))
    }
  },
  created () {
    fetch('https://dtv-projects.firebaseio.com/sections.json')
      .then((res) => { return res.json() })
      .then((res) => {
        this.dataGroup = res
      })

    eventBus.$on('favoriteItem', (fItem) => {
      var compare = false
      if (this.favorites.length) {
        this.favorites.map((favorite, i) => {
          if (favorite.url === fItem.url) {
            compare = true
            this.removeFavorites(i)
            return false
          } else {
          }
        })
        if (compare === false) {
          this.addFavorites(fItem)
        }
      } else {
        this.addFavorites(fItem)
      }
    })

    this.favorites = JSON.parse(localStorage.getItem('favories'))
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
