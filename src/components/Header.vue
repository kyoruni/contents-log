<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits(["changeTab"]);

const tabs = [
  { "name": "アニメ・映画・特撮", "value": "entertainment" },
  { "name": "本・漫画", "value": "book" },
  { "name": "ゲーム", "value": "game" }
];
const currentTab = ref("entertainment");

const changeTab = (selectTab: string) => {
  currentTab.value = selectTab;
  emit("changeTab", currentTab.value);
};
</script>

<template>
  <v-toolbar :color="'#f0f0f0'">
    <v-toolbar-title style="color: #da2b5c;"><a href="/">@kyoruni 見た・読んだ・遊んだリスト</a></v-toolbar-title>
    <v-spacer></v-spacer>
    <template v-slot:extension>
      <v-tabs centered>
        <v-tab v-for="tab in tabs" :key="tab.value" class="font-weight-bold" @click="changeTab(tab.value)">{{ tab.name }}</v-tab>
      </v-tabs>
    </template>
  </v-toolbar>
</template>

<style scoped lang="scss">
.v-toolbar-title__placeholder a {
  color: #da2b5c;
  text-decoration: none;
  &:hover {
    text-decoration: underline;
  }
}
</style>
