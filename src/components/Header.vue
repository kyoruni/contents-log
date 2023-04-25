<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits(["changeTab"]);

const tabs = [
  // { "name": "ゲーム", "value": "game" },
  { "name": "アニメ", "value": "anime" },
  // { "name": "まんが", "value": "comic" },
  { "name": "本", "value": "book" },
  // { "name": "映画", "value": "movie" },
];
const currentTab = ref("anime");

const changeTab = (selectTab: string) => {
  currentTab.value = selectTab;
  emit("changeTab", currentTab.value);
};
</script>

<template>
  <v-toolbar :color="'#f0f0f0'">
    <v-toolbar-title style="color: #da2b5c;">@kyoruni log</v-toolbar-title>
    <v-spacer></v-spacer>
    <template v-slot:extension>
      <v-tabs centered>
        <v-tab v-for="tab in tabs" :key="tab.value" class="font-weight-bold" @click="changeTab(tab.value)">{{ tab.name }}</v-tab>
      </v-tabs>
    </template>
  </v-toolbar>
</template>

