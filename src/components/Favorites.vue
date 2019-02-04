<template>
  <div class="section">
    <h3>Favoriler</h3>
    <div class="boxes">
      <ListItem
        v-for="favorite in favoritesdata"
        :key="favorite.id"
        :listitemdata="favorite"
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
  props: ['favoritesdata']
}
</script>
