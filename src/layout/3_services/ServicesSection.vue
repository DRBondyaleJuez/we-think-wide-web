<template>
    <div class="services">
        <h2>Servicios</h2>
        <div class="services-cards__wrapper">
            <div class="service-card" v-for="(servicesItem, index) in servicesList" :key="index">
                <service-card :service-card-content=servicesItem :index="index"></service-card>
            </div>
        </div>

    </div>
</template>
  
<script>
    import ServiceCard from "./ServiceCard.vue"
    import servicesCardList from './services-card-list.json';

  export default {
    name: "services-section",
    components: {
        ServiceCard
    },
    data() { 
        return {
            servicesList: servicesCardList
        };
    },
  };
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  </style>