<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Camera</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      <ion-button expand="block" @click="takePicture">
        <ion-icon slot="start" :icon="cameraOutline" />
        Take Picture
      </ion-button>

      <ion-text v-if="errorMessage" color="danger">
        <p>{{ errorMessage }}</p>
      </ion-text>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { Camera, CameraResultType, CameraSource } from '@capacitor/camera';
import {
  IonButton,
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
  IonIcon,
  IonText,
} from '@ionic/vue';
import { cameraOutline } from 'ionicons/icons';

const emit = defineEmits<{
  (event: 'photo-captured', photoDataUrl: string): void;
}>();

const errorMessage = ref('');

const takePicture = async () => {
  try {
    const photo = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.DataUrl,
      source: CameraSource.Camera,
    });

    if (photo.dataUrl) {
      emit('photo-captured', photo.dataUrl);
    }

    errorMessage.value = '';
  } catch (error) {
    errorMessage.value = error instanceof Error ? error.message : 'Unable to access the camera.';
  }
};
</script>

<style scoped>
ion-card {
  max-width: 420px;
  margin: 24px auto;
  border-radius: 18px;
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.12);
}

ion-card-header {
  padding-bottom: 8px;
}

ion-card-title {
  font-size: 1.3rem;
  font-weight: 600;
}

ion-button {
  --border-radius: 12px;
}

ion-text p {
  margin: 12px 0 0;
  font-size: 0.95rem;
  text-align: center;
}
</style>
