<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Capacitor Edge AI</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Capacitor Edge AI</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-grid>
        <ion-col>
          <ion-row>
            <ion-card v-if="!this.isCameraOn">
              <ion-card-header>
                <ion-card-title>AI at the tip of your fingers</ion-card-title>
              </ion-card-header>
              <ion-card-content>
               This demo app runs a real-time image classifier on your camera's feed
              </ion-card-content>
            </ion-card>
          </ion-row>
          <ion-row  v-if="!this.isCameraOn" class="ion-align-self-center ion-justify-content-center">
            <ion-button :onclick="() => startCamera(true)" color="primary">Front Camera</ion-button>
            <ion-button :onclick="() => startCamera(false)" color="primary">Rear Camera</ion-button>
          </ion-row>
          <ion-row  v-if="this.isCameraOn" class="ion-align-self-center ion-justify-content-center">
            <ion-button :onclick="stopCamera" color="primary">Stop Camera</ion-button>
          </ion-row>  
        </ion-col>
    </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCard, IonCardContent, IonCardTitle, IonCardHeader, IonGrid, IonCol, IonRow, IonButton } from '@ionic/vue';
import { CameraPreview, CameraPreviewOptions } from '@capacitor-community/camera-preview';


export default defineComponent({
  name: 'Tab1Page',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonCard, IonCardContent, IonCardTitle, IonCardHeader, IonGrid, IonCol, IonRow, IonButton },
  data: function () {
    return {
      modelReady: false,
      inferenceTime: 0,
      detectedClass: 'None',
      detectionConfidence: 0,
      isCameraOn: false
    }
  },
  methods: {
    async startCamera(frontCamera = false) {
      const cameraPreviewOptions: CameraPreviewOptions = {
        toBack: true,
        position: frontCamera ? 'front': 'rear',
        width: window.screen.width,
        height: 0.7 * window.screen.height,
        y: 0.7 * window.screen.height
      };
      await CameraPreview.start(cameraPreviewOptions);
      this.isCameraOn = true;
    },
    async stopCamera() {
      await CameraPreview.stop();
      this.isCameraOn = false
    },
  }
});
</script>

<style scoped>
ion-content {
  --background: transparent;
}
</style>