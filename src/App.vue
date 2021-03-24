<template>
  <div id="vue-app">
    <DynamicInput />
  </div>
</template>

<script>
import DynamicInput from "@/components/DynamicInput.vue";

export default {
  name: "vue-app",
  components: {
    DynamicInput
  }
};
</script>

<style>
#vue-app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
