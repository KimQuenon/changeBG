<script setup>
import { ref, onMounted } from 'vue';

const title = ref(null);
const redSection = ref(null);

const isInRedSection = ref(false);

onMounted(() => {
  const handleScroll = () => {
    const titleRect = title.value.getBoundingClientRect();
    const redSectionRect = redSection.value.getBoundingClientRect();

    if (
      titleRect.top <= redSectionRect.bottom &&
      titleRect.bottom >= redSectionRect.top
    ) {
      isInRedSection.value = true;
    } else {
      isInRedSection.value = false;
    }
  };

  window.addEventListener('scroll', handleScroll);


  onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll);
  });
});
</script>

<template>
  <div>
    <div class="bg1">
      <div ref="title" :class="{ 'white-text': isInRedSection }" class=" flex justify-between fixed top-1/2 -right-10 transform -translate-y-1/2 -rotate-90 z-50 ">
        <div class="p-2">          
          <p>Follow</p>
        </div>
        <div class="flex gap-1 p-2">          
          <p>FB.</p>
          <p>IG.</p>
          <p>LI.</p>
        </div>
      </div>
    </div>
    <div class="redSection" ref="redSection"></div>
    <div class="bg1"></div>
    <div class="bg1"></div>
  </div>
</template>

<style scoped>
.bg1 {
  height: 100vh;
}

.redSection {
  background-color: red;
  height: 100vh;
}

.white-text {
  color: white;
}
</style>
