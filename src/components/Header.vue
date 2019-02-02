<template>
  <div id="header">
    <div class="row">
      <div class="col-xs-12 col-md-9">
        <div class="nav">
          <a v-for="item in menuItems" href="/" :key="item.id">{{item.title}}</a>
        </div>
      </div>
      <div class="col-xs-12 col-md-3">
        <div class="search">
          <input type="text" placeholder="Arama" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      menuItems: []
    }
  },
  created () {
    fetch ('https://dtv-projects.firebaseio.com/menu.json')
      .then((res) => { return res.json() })
      .then((res) => {
        this.menuItems = res
      })
  }
}
</script>

<style lang="less">
.nav {
  a {
    font-size: 24px;
    padding: 6px 10px;
    transition: .2s;
    display: inline-block;
    margin-right: 20px;
    &:hover {
      background-color: #55a3ff;
    }
    &:last-child {
      margin-right: 0;
    }
    &.router-link-exact-active {
      background-color: #55a3ff;
    }
  }
}
.search {
  position: relative;
  opacity: .8;
  &:after {
    content: '';
    position: absolute;
    right: 10px;
    bottom: 8px;
    width: 15px;
    height: 16px;
    background: url('../assets/images/search.png');
  }
  input {
    color: #fff;
    background: none;
    font-size: 20px;
    border: none;
    border-bottom: 1px solid #fff;
    padding: 12px 40px 4px 10px;
    width: 100%;
    &::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
      color: #fff;
      opacity: 1; /* Firefox */
    }
    &:-ms-input-placeholder { /* Internet Explorer 10-11 */
      color: #fff;
    }
    &::-ms-input-placeholder { /* Microsoft Edge */
      color: #fff;
    }
  }
}
</style>
