<template>
  <MyCounter :limits="{init:10, end:20}"/>
</template>

<script>
import MyCounter from './components/MyCounter.vue'

export default {
  name: 'App',
  components: {
    MyCounter: MyCounter
  }
}
</script>

<style scoped>
</style>
