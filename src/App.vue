<template>
  <MyForm/>
  <MyCounters :nb="3"/>
</template>

<script setup>
import MyCounters from './components/MyCounters.vue';
import MyForm from './components/MyForm.vue';

// export default {
//   name: 'App',
//   components: {
//     MyCounters: MyCounters
//   }
// }
</script>

<style scoped>
</style>
