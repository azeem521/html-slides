<template>
  <div class="image-container" @click="nextImage">
    <TransitionGroup name="fade">
      <img
        v-for="(image, index) in images"
        :key="image"
        :src="image"
        :alt="`Image ${index + 1}`"
        v-show="currentIndex === index"
        class="transition-image"
      />
    </TransitionGroup>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  images: {
    type: Array,
    required: true,
  },
});

const currentIndex = ref(0);

const nextImage = () => {
  currentIndex.value = (currentIndex.value + 1) % props.images.length;
};
</script>

<style scoped>
.image-container {
  position: relative;
  width: 100%;
  height: 400px; /* Adjust as needed */
  cursor: pointer;
}

.transition-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
