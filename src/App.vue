<template>
 <main>
    <HeaderView />
    <MediaInteractiveDisplay />
    <div class="content-wrapper">
      <h3 class="introduction">
        {{ introduction.text }}
      </h3>
      <ServicesSection />
      <SpecializedServices />
      <ProjectsSection />
      <InterihotelSection />
      <EcosystemSection />
      <ClientsSection />
    </div>
    <FooterView />
  </main>
</template>

<script>
import HeaderView from './layout/1_header/HeaderView.vue'

import MediaInteractiveDisplay from './layout/2_media_interactive_display/MediaInteractiveDisplay.vue'
import ServicesSection from './layout/3_services/ServicesSection.vue'
import SpecializedServices from './layout/4_specialized_services/SpecializedServices.vue'
import ProjectsSection from './layout/5_projects/ProjectsSection.vue'
import InterihotelSection from './layout/6_interihotel/InterihotelSection.vue'
import EcosystemSection from './layout/7_ecosystem/EcosystemSection.vue'
import ClientsSection from './layout/8_clients/ClientsSection.vue'
import FooterView from './layout/9_footer/FooterView.vue'


import introduction from './assets/static/json/introduction.json';


export default {
  name: 'App',
  components: {
    HeaderView,
    MediaInteractiveDisplay,
    ServicesSection,
    SpecializedServices,
    ProjectsSection,
    InterihotelSection,
    EcosystemSection,
    ClientsSection,
    FooterView


  },
  data() { 
      return {
        introduction: introduction
      };
    },
}
</script>

<style>
</style>
