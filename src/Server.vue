<template>
  <li 
    class="list-group-item"
    @click="serverSelected"
    :class="{
      'list-group-item-warning': server.status === 'Degraded',
      'list-group-item-danger': server.status === 'Critical',
      'list-group-item-success': server.status === 'Normal'
    }">
    Server #{{ server.id }}
  </li>  
</template>

<script>
  export default {
    props: {
      server: {
        type: Object,
        required: true
      }
    },

    methods: {
      serverSelected() {
        this.$emit("serverSelected", this.server.id);
      }
    }
  }
</script>

<style scoped>
  li {
    cursor: pointer;
  }

  li:hover {
    background-color: lightgray;
  }
</style>
