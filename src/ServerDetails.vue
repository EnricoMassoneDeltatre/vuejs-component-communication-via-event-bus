<template>
  <div v-if="server">
    <h3>Server {{ server.id }}</h3>
    <form>
      <div class="form-group">
        <label>Status</label>
        <select 
          class="form-control"
          @change="serverStatusChanged">
          <option
            v-for="status in statuses"
            :key="status"
            :value="status"
            :selected="status === server.status">
            {{ status }}
          </option>
        </select>
      </div>
    </form>
  </div>

  <div v-else>
    <h3>
      No server selected
    </h3>
  </div>
</template>

<script>
  import { eventBus } from "./main";

  export default {
    data: function() {
      return {
        statuses: ["Normal", "Degraded", "Critical"],
        server: null
      };
    },

    methods: {
      serverStatusChanged(event) {
        const newServerStatus = event.target.value;
        const { id: serverId } = this.server;

        this.server.status = newServerStatus;

        eventBus.$emit("serverStatusChanged", {
          serverId,
          status: newServerStatus
        });
      }
    },

    created() {
      eventBus.$on("serverSelected", selectedServer => {
        this.server = selectedServer;
      });
    }
  }
</script>

<style>
</style>