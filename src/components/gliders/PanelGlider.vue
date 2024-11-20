<template>
    <div class="panel__glider">
        <div :class="`glide-${index}`">
            <div class="glide__track" data-glide-el="track">
                <ul class="glide__slides">

                    <div v-for="(panelItem, index) in panelContent" :key="index">

                        <li class="glide__slide">
                            <div class="panel-content">
                                <img
                                class="panel-content__image"
                                :src="panelItem.image"
                                :alt="`Panel_Image_${index + 1}`"
                                >
                                <h4 class="panel-content__text">
                                    {{ panelItem.text }}
                                </h4>
                            </div>
                        </li>
                        
                    </div>
                </ul>
            </div>

            <div class="glide__arrows" data-glide-el="controls">
                <!-- <button class="glide__arrow glide__arrow--left" data-glide-dir="<">prev</button>            -->
                <button class="glide__arrow glide__arrow--right" data-glide-dir=">">
                    <img src="../../assets/static/icons/arrow-right.png">
                </button>
            </div>

        </div>   
    </div>
</template>

<script>
    import Glide from '@glidejs/glide';

    export default {
    name: "PanelGlider",
    props: {
        panelContent: {
            type: Array,
            required: true
        },
        index: {
            type: Number,
            required: true
        }
    },
    data() { 
        return {
        };
    },
    mounted() {
        this.setGlider();
    }, 
    methods: {
        setGlider() {
            const config = {
                type: 'carousel',
                startAt: 0,
                perView: 1,
                gap: 0

            }
            new Glide('.glide-'+this.index, config).mount({})

        },
    }   
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>