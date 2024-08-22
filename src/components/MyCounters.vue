<script setup>
import MyCounter from './MyCounter.vue'
import { defineProps } from 'vue';

defineProps(["nb"]);
</script>

<template>
  <MyCounter v-for="i in nb" v-bind:key="i" :limits="{init:10, end:20}"/>
</template>
