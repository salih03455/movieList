<template>
  <div class="section">
    <h3>{{ listdata.title }}</h3>
    <div class="boxes">
      <ListItem
        v-for="listitem in listdata.data"
        :key="listitem.id"
        :listitemdata="listitem"
      />
    </div>
  </div>
</template>

<script>
import ListItem from '@/components/ListItem'

export default {
  components: {
    ListItem
  },
  props: ['listdata']
}
</script>

<style lang="less">
.section {
  h3 {
    font-size: 36px;
    opacity: .8;
    font-weight: 400;
  }
}

.boxes {
  display: flex;
  flex-wrap: wrap;
}
</style>
