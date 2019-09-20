<template>
  <div class="row">
      <div class="col-xs-12 col-sm-6">
          <my-server-list ></my-server-list>
      </div>
      <div class="col-xs-12 col-sm-6">
          <my-server-details 
            :server="selectedServer"
            @serverStatusChanged="onServerStatusChanged">

          </my-server-details>
      </div>
  </div>
</template>

<script>
  import ServerDetails from "./ServerDetails.vue";
  import ServerList from "./ServerList.vue";

  export default {
    data: function() {
      return {
        selectedServer: null
      }
    },

    methods: {
      onServerStatusChanged(eventData) {
        const {serverId, status: updatedStatus} = eventData;
        
        this.servers = this.servers.map(server => {
          if (server.id === serverId) {
            return {
              id: server.id,
              status: updatedStatus
            };
          } else {
            return server;
          }
        });

        if (this.selectedServer) {
          this.selectedServer = this.servers.find(server => server.id === this.selectedServer.id);
        }
      }
    },

    components: {
      "my-server-details": ServerDetails,
      "my-server-list": ServerList
    }
  };
</script>

<style>
</style>