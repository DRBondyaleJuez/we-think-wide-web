<template>
  <div class="clients">
    <h2>Clientes</h2>
    <div class="clients-list">
        <ul>
          <li v-for="(clientInfo, index) in clientList" :key="index">
            {{ clientInfo }}
          </li>
        </ul>
    </div>
  </div>
</template>

<script>
  import clientInfoList from './client-list.json';

  export default {
    name: "clients-section",
    data() { 
      return {
        clientList: clientInfoList
      };
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>