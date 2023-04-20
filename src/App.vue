<script setup lang="ts">
import { ref } from "vue";

import Header from '@/components/Header.vue';
import ContentsList from '@/components/ContentsList.vue';

const currentTab = ref("anime");

const changeTab = (selected: string) => {
  currentTab.value = selected;
};
</script>

<template>
  <v-app>
    <v-main>
      <v-container fluid class="pa-0">
        <Header @changeTab="changeTab"/>
        <ContentsList :category="currentTab"/>
      </v-container>
    </v-main>
  </v-app>
</template>
