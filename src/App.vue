<template>
  <div id="app">
    <app-header></app-header>
    <app-booklist></app-booklist>
  </div>
</template>

<script>
import Booklist from "./components/booklist.vue";
import Header from "./components/header.vue";
export default {
  components: {
    "app-booklist": Booklist,
    "app-header": Header
  }
};
</script>

<style>
body {
  font-family: Arial;
  margin-right: 5%;
  margin-left: 5%;
  margin-bottom: 20px;
  background-color: rgb(102, 102, 102);
}
</style>