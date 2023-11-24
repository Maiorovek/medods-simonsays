<template>
  <div id="app">
    <CustomHeader/>
    <SimonSays/>
  </div>
</template>

<script>
import SimonSays from './components/Simon-Says.vue';
import CustomHeader from './components/UI/Custom-Header.vue';


export default {
  name: 'App',
  components: {
    SimonSays,
    CustomHeader,
}
}
</script>

<style> </style>
