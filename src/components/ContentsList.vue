<script setup lang="ts">
import { ref, onMounted } from "vue";
import animeList from "@/assets/json/anime.json";

const props = defineProps({
  category: {
    type: String,
    required: false,
    default: "anime"
  }
});

interface AnimeData {
  id: number;
  title: string;
  episode: string;
  subtitle: string;
  airdate: string;
  watcheddate: string;
  impression: string;
  tags: string[];
};

const contents = ref<AnimeData[]>([]);

onMounted(() => {
  switch (props.category) {
    case "anime":
      contents.value = animeList;
      break;
    default:
      contents.value = [];
  };
});
</script>
<template>
  {{ contents }}
</template>