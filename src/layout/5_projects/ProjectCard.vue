<template>
    <div class="project-card__wrapper">
        <card-glider :card-content="projectCardContent.cardContent" :index="'project'+index"></card-glider>
        <h3 class="project-card__title">
            {{ projectCardContent.title }}
        </h3>
        <p class="project-card__description">
            {{ projectCardContent.description }}
        </p>

    </div>
</template>
  
<script>
    import CardGlider from "../../components/gliders/CardGlider.vue"

    export default {
        name: "ProjectCard",
        props: {
            projectCardContent: {
                type: Object,
                required: true
            },
            index: {
                type: Number,
                required: true
            }
        },
        components: {
            CardGlider
        }
    };
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

  </style>
  