<template>
  <div class="row">
      <div class="col-xs-12 col-sm-6">
          <my-server-list 
            :servers="servers"
            @selectedServerChanged="onSelectedServerChanged">

          </my-server-list>
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
        selectedServer: null,
        servers: [
          { id: 1, status: "Normal" },
          { id: 2, status: "Critical" },
          { id: 3, status: "Degraded" },
          { id: 4, status: "Critical" },
          { id: 5, status: "Normal" }
        ]
      }
    },

    methods: {
      onSelectedServerChanged(eventData) {
        const selectedServer = this.servers.find(server => server.id === eventData);
        if (!selectedServer) {
          throw new Error(`Unable to find a server having id ${eventData}`);
        }

        this.selectedServer = selectedServer;
      },

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