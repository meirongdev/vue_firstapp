<template>
  <MyCounters :nb="3"/>
</template>

<script >
import MyCounters from './components/MyCounters.vue'

export default {
  name: 'App',
  components: {
    MyCounters: MyCounters
  }
}
</script>

<style scoped>
</style>
