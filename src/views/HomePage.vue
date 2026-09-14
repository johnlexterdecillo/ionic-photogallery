<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <div class="page-content">
        <div class="content-stack">
          <CameraComponent @photo-captured="handlePhotoCaptured" />
          <PhotoGalleryComponent :photos="photos" />
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
} from '@ionic/vue';
import CameraComponent from '@/components/CameraComponent.vue';
import PhotoGalleryComponent from '@/components/PhotoGalleryComponent.vue';

const photos = ref<string[]>([]);

const handlePhotoCaptured = (photoDataUrl: string) => {
  photos.value = [photoDataUrl, ...photos.value];
};
</script>

<style scoped>
.page-content {
  min-height: 100%;
  padding: 24px 16px 40px;
}

.content-stack {
  max-width: 960px;
  margin: 0 auto;
}
</style>
