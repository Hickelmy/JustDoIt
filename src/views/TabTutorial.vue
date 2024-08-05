<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-card color="light">
            <div class="image-container">
              <img alt="Silhouette of mountains" src="../img/work.jpg" />
            </div>
            <ion-card-header>
            
              <ion-card-subtitle>
                Ao fazer uma lista de tarefas, você saberá as prioridades que deseja trabalhar, para que fique mais estruturado na execução do seu trabalho.
              </ion-card-subtitle>
              <ion-card-title>Gerencie seu dia a dia</ion-card-title>
            </ion-card-header>
            <ion-button expand="block" class="next-button">Avançar</ion-button>
          </ion-card>
        </ion-toolbar>
      </ion-header>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCard, IonCardHeader, IonCardTitle, IonCardSubtitle, IonButton } from '@ionic/vue';
</script>

<style scoped>
.image-container {
  height: 60vh; /* 60% da tela */
  overflow: hidden;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.next-button {
  margin-top: 16px;
  margin-left: auto;
  margin-right: auto;
}
</style>
