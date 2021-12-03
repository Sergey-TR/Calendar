<template>
  <div id="app">
    <Calendar />
  </div>
</template>

<script>
import Calendar from "./components/Calendar";

export default {
  name: 'App',
  components: {
   Calendar
  }
}
</script>

<style>
#app {
  padding: 40px 60px;
}
.btn {
  border: none;
  outline: none;
  background: none;
  cursor: pointer;
}
</style>
