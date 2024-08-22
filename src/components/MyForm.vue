<script setup>
  import { ref } from 'vue';
  const name = ref('');
  let dates = [];
  for (let year=2024; year > 1900; year--) {
    dates.push(year);
  }
  const birthYear = ref('');
  const maritalStatus = ref("");
</script>

<template>
  <form>
    <label for="name">Name:</label>
    <input type="text" id="name" v-model.lazy="name" />
    <label for="birthYear">Birth Year:</label>
    <select id="birthYear" v-model="birthYear">
      <option v-for="date in dates" :key="date" :value="date">{{ date }}</option>
    </select>

  Marital Status:
  <input type="radio" id="single" name="maritalStatus" value="single" v-model="maritalStatus">
  <label for="single">Single</label>
  <input type="radio" id="married" name="maritalStatus" value="married" v-model="maritalStatus">
  <label for="married">Married</label>
  </form>
  <h3> Reactive Variables</h3>
  <p>Name: {{ name }}</p>
  <p>Birth Year: {{ birthYear }}</p>
  <p>Marital Status: {{ maritalStatus }}</p>


</template>