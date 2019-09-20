<template>
  <ul class="list-group">
      <my-server 
        v-for="server in servers" 
        :key="server.id"
        :server="server"
        @click.native="serverSelected(server.id)">
      </my-server>
  </ul>  
</template>

<script>
  import Server from "./Server.vue";
  import { eventBus } from "./main";
  import { cloneDeep } from "lodash";

  export default {
    data: function() {
      return {
        servers: [
          { id: 1, status: "Normal" },
          { id: 2, status: "Critical" },
          { id: 3, status: "Degraded" },
          { id: 4, status: "Critical" },
          { id: 5, status: "Normal" }
        ]
      };
    },

    methods: {
      serverSelected(selectedServerId) {
        const selectedServer = this.servers.find(server => server.id === selectedServerId);
        if (!selectedServer) {
          throw new Error(`Unable to find a server having id ${selectedServerId}`);
        }

        eventBus.$emit('serverSelected', cloneDeep(selectedServer));
      }
    },

    components: {
      "my-server": Server
    }
  };
</script>

<style></style>
