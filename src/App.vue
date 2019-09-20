<template>
    <div class="container">
        <my-header></my-header>
        <hr>
        <my-server-dashboard></my-server-dashboard>
        <hr>
        <my-footer></my-footer>
    </div>
</template>

<script>
  import Header from "./Header.vue";
  import Footer from "./Footer.vue";
  import ServerDashboard from "./ServerDashboard.vue";

  export default {
    components: {
      "my-header": Header,
      "my-footer": Footer,
      "my-server-dashboard": ServerDashboard
    }
  }
</script>

<style>
</style>
