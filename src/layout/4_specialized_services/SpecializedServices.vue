<template>
    <div class="specialized-services">
        <h2>Servicios especializados</h2>
        <h4>Consultoría y estudio de diseño para hoteles</h4>
        <panel-glider :panel-content="specializedServiceContentList" :index="'specialized-service'+index"></panel-glider>
    </div>
</template>
  
<script>
    import PanelGlider from "../../components/gliders/PanelGlider.vue"
    import specializedServicePanelList from './specialized-services-panel-list.json';

  export default {
    name: "Special-Services",
    components: {
        PanelGlider
    },
    data() { 
        return {
            specializedServiceContentList: specializedServicePanelList
        };
    }
  };
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  </style>