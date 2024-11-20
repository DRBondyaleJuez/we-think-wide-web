<template>
    <div class="projects">
        <h2>Proyectos Seleccionados</h2>
        <div class="projects-cards__wrapper">
            <div class="project-card" v-for="(projectItem, index) in projectList" :key="index">
                <project-card :project-card-content=projectItem :index="index"></project-card>
            </div>
        </div>

    </div>
</template>
  
<script>
    import ProjectCard from "./ProjectCard.vue"
    import projectsCardList from './project-card-list.js';

  export default {
    name: "projects-section",
    components: {
        ProjectCard
    },
    data() { 
        return {
            projectList: projectsCardList
        };
    },
  };
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  </style>