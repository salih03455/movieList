<template>
  <div class="box">
    <div class="box-inside">
      <img :src="getImgUrl()" >
      <div class="box-ex">
        <div class="fav-button" @click="addFav"></div>
        <div class="text-area">
          <div class="name">{{ listitemdata.title }}</div>
          <div class="description">{{ listitemdata.subTitle }}</div>
          <div class="year">{{ getYear() }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main'

export default {
  props: ['listitemdata'],
  methods: {
    getImgUrl () {
      let images = require.context('../assets/images/movies', false)
      return images('./' + this.listitemdata.image.toLowerCase())
    },
    getYear () {
      return this.listitemdata.published_date.split('-')[0]
    },
    addFav () {
      eventBus.$emit('favoriteItem', this.listitemdata)
    }
  }
}
</script>

<style lang="less">
@import  '../assets/less/variables.less';

.box {
  flex: 0 25%;
  padding-right: 20px;
  margin-bottom: 20px;
  @media @tablet {
    flex: 0 33.3333%;
    &:nth-child(2n) {
      padding-right: 20px;
    }
    &:nth-child(3n) {
      padding-right: 0;
    }
  }
  @media @mobile {
    flex: 0 50%;
    &:nth-child(2n) {
      padding-right: 0;
    }
    &:nth-child(3n) {
      padding-right: 20px;
    }
  }
  @media @desktop {
    &:nth-child(4n) {
      padding-right: 20px;
    }
  }
  .box-inside {
    position: relative;
    img {
      display: block;
      width: 100%;
      height: 370px;
      overflow: hidden;
    }
    .box-ex {
      position: absolute;
      width: 100%;
      height: 100%;
      left: 0;
      top: 0;
      background-color: rgba(0, 0, 0, 0.4);
      line-height: 25px;
      transition: .2s;
      opacity: 0;
      .fav-button {
        position: absolute;
        right: 20px;
        top: 15px;
        width: 31px;
        height: 31px;
        border-radius: 50%;
        box-shadow: 0 0 0 1px #fff;
        cursor: pointer;
        transition: .2s;
        &:before,
        &:after {
          content: '';
          display: block;
          width: 10px;
          height: 2px;
          position: absolute;
          background-color: #fff;
        }
        &:before {
          left: 10px;
          top: 14px;
        }
        &:after {
          left: 10px;
          top: 14px;
          transform: rotate(90deg);
        }
        &:hover {
          background-color: #55a3ff;
          transform: rotate(45deg);
        }
      }
      .text-area {
        position: absolute;
        left: 10px;
        bottom: 10px;
        font-size: 22px;
        .year {
          font-size: 18px;
          font-weight: 700;
        }
      }
    }
    &:hover {
      .box-ex {
        opacity: 1;
      }
    }
  }
}
</style>
