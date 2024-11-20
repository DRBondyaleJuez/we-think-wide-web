<template>
    <div class="media-interactive-display">
        <div class="media-wrapper">
            <multi-media-displayer
                :mediaItems = "mediaList"
                :autoPlayInterval="5000"
                :containerWidth="1000"
            ></multi-media-displayer>
        </div>
    </div>
</template>

<script>
import MultiMediaDisplayer from "../../components/MultiMediaDisplayer.vue"

import mediaInteractiveList from './media-interactive-list.json';

export default {
    name: "VideoInteractiveDisplay",
    components: {
        MultiMediaDisplayer
    },
    data() { 
        return {
            mediaList: mediaInteractiveList
        };
    } 
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.media-interactive-display {
    .media-wrapper {
        position: relative;
    }
}
</style>