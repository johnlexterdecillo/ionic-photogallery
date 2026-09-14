<template>
  <ion-card class="gallery-card">
    <ion-card-header>
      <ion-card-title>Gallery</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      <div v-if="photos.length" class="gallery-grid">
        <div v-for="(photo, index) in photos" :key="`${photo}-${index}`" class="photo-item">
          <img :src="photo" :alt="`Captured photo ${index + 1}`" />
        </div>
      </div>

      <div v-else class="empty-state">
        <ion-icon :icon="imagesOutline" />
        <p>No photos yet.</p>
      </div>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
  IonIcon,
} from '@ionic/vue';
import { imagesOutline } from 'ionicons/icons';

const props = defineProps<{
  photos: string[];
}>();
</script>

<style scoped>
.gallery-card {
  margin-top: 24px;
  border-radius: 18px;
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.12);
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 12px;
}

.photo-item {
  border-radius: 12px;
  overflow: hidden;
  background: #f4f4f4;
  aspect-ratio: 1;
}

.photo-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  min-height: 180px;
  color: #666;
}

.empty-state ion-icon {
  font-size: 2.5rem;
  margin-bottom: 8px;
}

.empty-state p {
  margin: 0;
}
</style>
