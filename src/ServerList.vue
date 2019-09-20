<template>
  <ul class="list-group">
      <my-server 
        v-for="server in servers" 
        :key="server.id"
        :server="server"
        @serverSelected="onSelectedServerChanged">
      </my-server>
  </ul>  
</template>

<script>
  import Server from "./Server.vue";
  import { eventBus } from "./main";

  export default {
    props: {
      servers: {
        type: Array,
        required: true
      }
    },

    methods: {
      onSelectedServerChanged(eventData) {
        this.$emit("selectedServerChanged", eventData);
      }
    },

    components: {
      "my-server": Server
    }
  };
</script>

<style></style>
