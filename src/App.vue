<template>
  <MyForm/>
  <MyCounters :nb="2"/>
  <br/><hr/><br/>
  Overall Total increased from App: <b>{{total}}</b>
</template>

<script setup>
import { ref, provide } from 'vue';
import MyCounters from './components/MyCounters.vue';
import MyForm from './components/MyForm.vue';

const total = ref(0);
provide('app.total', total);
// export default {
//   name: 'App',
//   components: {
//     MyCounters: MyCounters
//   }
// }
</script>

<style scoped>
</style>
