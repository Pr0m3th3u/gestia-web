<script setup lang="ts">

import UploadImage from './components/UploadImage.vue'
import UploadImageLayout from './layouts/UploadimageLayout.vue';
import ImageGallery from './components/ImagesGallery.vue';

</script>

<template>
  <div>
    <UploadImageLayout>
      <template #header>
          Sharing you happy, bro! ;)
      </template>

      <UploadImage />
    </ UploadImageLayout>
  </div>
  <ImageGallery />
</template>

<style>

.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
