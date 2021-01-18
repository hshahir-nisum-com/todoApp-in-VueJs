<template>
  <FormTodo />
</template>

<script>
import FormTodo from "./components/todoForm.vue";

export default {
  name: "App",
  components: {
    FormTodo,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
