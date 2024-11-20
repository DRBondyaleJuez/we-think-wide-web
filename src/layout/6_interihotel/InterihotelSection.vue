<template>
  <div class="interihotel">
      <h2>Interihotel</h2>
      <panel-glider :panel-content="interihotelContentList" :index="'interihotel'+index"></panel-glider>
  </div>
</template>

<script>
  import PanelGlider from "../../components/gliders/PanelGlider.vue"
  import interihotelPanelList from './interihotel-panel-list.json';

export default {
  name: "interihotel-section",
  components: {
      PanelGlider
  },
  data() { 
      return {
          interihotelContentList: interihotelPanelList
      };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>