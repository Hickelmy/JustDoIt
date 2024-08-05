<template>
  <ion-page>
    <ion-menu content-id="main-content" side="start">
      <ion-header>
        <ion-toolbar>
          <ion-title>Menu</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <ion-list>
          <ion-item button @click="navigateTo('/profile')">
            <ion-label>Perfil</ion-label>
          </ion-item>
          <ion-item button @click="navigateTo('/settings')">
            <ion-label>Configurações</ion-label>
          </ion-item>
          <ion-item button @click="logout">
            <ion-label>Logout</ion-label>
          </ion-item>
        </ion-list>
        <ion-menu-toggle>
          <ion-button expand="block">Fechar menu</ion-button>
        </ion-menu-toggle>
      </ion-content>
    </ion-menu>

    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button></ion-menu-button>
        </ion-buttons>
        <ion-title>Tab 1</ion-title>
        <ion-buttons slot="end">
          <ion-avatar @click="presentPopover($event)">
            <img alt="Silhouette of a person's head" src="https://ionicframework.com/docs/img/demos/avatar.svg" />
          </ion-avatar>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>

    <ion-content id="main-content" :fullscreen="true" class="ion-padding">
      <ion-refresher slot="fixed" @ionRefresh="handleRefresh($event)">
        <ion-refresher-content></ion-refresher-content>
      </ion-refresher>

      <div class="center-content">
        <h1>Hi Rick</h1>
        <h2>Estas são suas atividades</h2>
        <ion-searchbar placeholder="Pesquisar por"></ion-searchbar>

        <div class="mini-tasks-header">
          <h3>Mini-Task</h3>
          <ion-button fill="clear" class="view-more">View More</ion-button>
        </div>

        <swiper-container class="mini-tasks-slider" slides-per-view="3" space-between="10">
          <swiper-slide v-for="i in 6" :key="i">
            <ion-card class="mini-task-card">
              <ion-card-header>
                <ion-card-title>Tarefa {{ i }}</ion-card-title>
              </ion-card-header>
              <ion-card-content>
                Descrição da tarefa {{ i }}
              </ion-card-content>
            </ion-card>
          </swiper-slide>
        </swiper-container>
      </div>
    </ion-content>

    <ion-popover :is-open="popoverOpen" :event="popoverEvent" @ionPopoverDidDismiss="popoverOpen = false">
      <ion-content>
        <ion-list>
          <ion-item button @click="navigateTo('/profile')">Perfil</ion-item>
          <ion-item button @click="navigateTo('/settings')">Configurações</ion-item>
          <ion-item button @click="logout">Logout</ion-item>
        </ion-list>
      </ion-content>
    </ion-popover>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonMenu, IonButtons, IonMenuButton, IonAvatar, IonPopover, IonList, IonItem, IonButton, IonMenuToggle, IonLabel, IonSearchbar, IonCard, IonCardHeader, IonCardTitle, IonCardContent } from '@ionic/vue';
import { useRouter } from 'vue-router';
import { register } from 'swiper/element/bundle';

register();

const router = useRouter();
const popoverOpen = ref(false);
const popoverEvent = ref<Event | null>(null);

const handleRefresh = (event: CustomEvent) => {
  setTimeout(() => {
    event.target.complete();
  }, 2000);
};

const presentPopover = (ev: Event) => {
  ev.stopPropagation();
  popoverEvent.value = ev;
  popoverOpen.value = true;
};

const navigateTo = (route: string) => {
  popoverOpen.value = false;
  router.push(route);
};

const logout = () => {
  popoverOpen.value = false;
  console.log('Logging out');
};
</script>

<style scoped>
.center-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0 20px;
}

ion-avatar {
  cursor: pointer;
}

.mini-tasks-header {
  display: flex;
  justify-content: space-between;
  width: 100%;
  align-items: center;
  margin-top: 20px;
}

.mini-tasks-header h3 {
  margin: 0;
}

.view-more {
  color: grey;
}

.mini-tasks-slider {
  width: 100%;
  margin-top: 10px;
}

.mini-task-card {
  width: 150px;
  height: 100px;
  margin: 0 10px;
}
</style>
