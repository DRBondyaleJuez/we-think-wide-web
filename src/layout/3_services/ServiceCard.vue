<template>
    <div class="service-card__wrapper" :id="index">
        <card-glider :cardContent="serviceCardContent.cardContent" :index="'service'+index"></card-glider>
    </div>
</template>
  
<script>
    import CardGlider from "../../components/gliders/CardGlider.vue"

    export default {
        name: "ServiceCard",
        props: {
            serviceCardContent: {
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
        },
        mounted() {
            console.log(this.projectCardContent);
        }
    };
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

  </style>
  