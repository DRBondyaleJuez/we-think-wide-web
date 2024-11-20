<template>
    <div class="multi-media-displayer">
        <div class="multi-media-displayer__wrapper"
            ref="containerRef"
            :style="{ width: `100%`, height: `${containerWidth * 0.7}px` }"
            @mouseenter="handleMouseEnter"
            @mouseleave="handleMouseLeave"
            @mousemove="handleMouseMove"
        >
            <template v-for="(item, index) in mediaItems" :key="index">
              <!-- Image -->
              <img
                v-if="item.type === 'image'"
                :src="item.url"
                :alt="`Media item ${index + 1}`"
                class="multi-media-displayer__view multi-media-displayer__view--img"
                :class="{ 'opacity-0': currentIndex !== index }"
              >
              
              <!-- Video -->
              <video
                v-else-if="item.type === 'video'"
                :src="item.url"
                class="multi-media-displayer__view multi-media-displayer__view--video"
                :class="{ 'opacity-0': currentIndex !== index }"
                :poster="item.thumbnail"
                loop
                muted
                :autoplay="currentIndex === index"
              />
              
              <!-- GIF -->
              <img
                v-else-if="item.type === 'gif'"
                :src="item.url"
                :alt="`Gif item ${index + 1}`"
                class="multi-media-displayer__view multi-media-displayer__view--gif"
                :class="{ 'opacity-0': currentIndex !== index }"
              >
            </template>
          </div>
    </div>
</template>

<script>
import { ref, onMounted, onBeforeUnmount } from 'vue';

export default {
  name: 'MultiMediaDisplayer',
  props: {
    mediaItems: {
      type: Array,
      required: true,
    },
    autoPlayInterval: {
      type: Number,
      default: 3000 // 3 seconds
    },
    containerWidth: {
      type: Number,
      default: 800
    }
  },

  setup(props) {
    const currentIndex = ref(0);
    const containerRef = ref(null);
    const autoPlayTimer = ref(null);
    const isHovering = ref(false);

    const calculateIndexFromMousePosition = (event) => {
      if (!containerRef.value) return;
      
      const rect = containerRef.value.getBoundingClientRect();
      const relativeX = event.clientX - rect.left;
      const segmentWidth = rect.width / props.mediaItems.length;
      const newIndex = Math.floor(relativeX / segmentWidth);
      
      currentIndex.value = Math.max(0, Math.min(newIndex, props.mediaItems.length - 1));
    };

    const startAutoPlay = () => {
      if (!isHovering.value) {
        autoPlayTimer.value = setInterval(() => {
          currentIndex.value = (currentIndex.value + 1) % props.mediaItems.length;
        }, props.autoPlayInterval);
      }
    };

    const stopAutoPlay = () => {
      if (autoPlayTimer.value) {
        clearInterval(autoPlayTimer.value);
        autoPlayTimer.value = null;
      }
    };

    const handleMouseEnter = () => {
      isHovering.value = true;
      stopAutoPlay();
    };

    const handleMouseLeave = () => {
      isHovering.value = false;
      startAutoPlay();
    };

    const handleMouseMove = (event) => {
      if (isHovering.value) {
        calculateIndexFromMousePosition(event);
      }
    };

    onMounted(() => {
      startAutoPlay();
    });

    onBeforeUnmount(() => {
      stopAutoPlay();
    });

    return {
      currentIndex,
      containerRef,
      handleMouseEnter,
      handleMouseLeave,
      handleMouseMove,
    };
  }
};
</script>

<style scoped>

.multi-media-displayer {
  width: 100%;
  height: 700px;

  &__view {
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: center;
      position: absolute;
  }

  .opacity-0 {
      opacity: 0;
  }
}

</style>