<template>
  <div class="row">
      <div class="col-xs-12 col-sm-6">
          <my-server-list></my-server-list>
      </div>
      <div class="col-xs-12 col-sm-6">
          <my-server-details></my-server-details>
      </div>
  </div>
</template>

<script>
  import ServerDetails from "./ServerDetails.vue";
  import ServerList from "./ServerList.vue";

  export default {
    components: {
      "my-server-details": ServerDetails,
      "my-server-list": ServerList
    }
  };
</script>

<style></style>