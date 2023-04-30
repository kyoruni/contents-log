<script setup lang="ts">
import { ref, onBeforeMount, watch } from "vue";
import entertainmentList from "@/assets/json/entertainment.json";
import bookList from "@/assets/json/book.json";
import gameList from "@/assets/json/game.json";
import { propsToAttrMap } from "@vue/shared";

const props = defineProps({
  category: {
    type: String,
    required: false,
    default: "entertainment"
  }
});

const itemsPerPage = 100;

interface EntertainmentData {
  id: number;
  title: string;
  episode: string;
  subtitle: string;
  airdate: string;
  watcheddate: string;
  impression: string;
};

interface BookData {
  id: number;
  title: string;
  publisher: string;
  author: string;
  page: number;
  publishDate: string;
  buyDate: string;
  startDate: string;
  endDate: string;
  category: string;
  type: string;
  impression: string;
};

interface GameData {
  id: number;
  title: string;
  developer: string;
  release_date: string;
  genre: string;
  summary: string;
  play_time: string;
  start_date: string;
  end_date: string;
  impression: string;
  memo: string;
};

interface Table {
  title: string;
  align: string;
  sortable: boolean;
  key: string;
  width: string;
}

const contents = ref<EntertainmentData[] | BookData[] | GameData[]>([]);
const headers = ref<Table[]>([]);

onBeforeMount(() => {
  fetchItemList();
});

watch(
  () => props.category,
  () => {
    fetchItemList();
  }
);

const fetchItemList = () => {
  switch (props.category) {
    case "entertainment":
      contents.value = entertainmentList;
      headers.value = [
        { title: "タイトル", align: 'start', sortable: true, key: "title", width: "100px" },
        { title: "話数", align: 'start', sortable: true, key: "episode", width: "50px"},
        { title: "サブタイトル", align: 'start', sortable: true, key: "subtitle", width: "100px" },
        { title: "放送日", align: 'start', sortable: true, key: "airdate", width: "50px" },
        { title: "視聴日", align: 'start', sortable: true, key: "watcheddate", width: "50px" },
        { title: "カテゴリー", align: 'start', sortable: true, key: "category", width: "100px" },
        { title: "ひとこと", align: 'start', sortable: true, key: "impression", width: "200px" },
      ];
      break;
    case "book":
      contents.value = bookList;
      headers.value = [
        { title: "タイトル", align: 'start', sortable: true, key: "title", width: "200px" },
        { title: "出版社", align: 'start', sortable: true, key: "publisher", width: "1px"},
        { title: "著者", align: 'start', sortable: true, key: "author", width: "1px" },
        { title: "ページ数", align: 'start', sortable: true, key: "page", width: "1px" },
        { title: "出版日", align: 'start', sortable: true, key: "publishDate", width: "1px" },
        { title: "購入日", align: 'start', sortable: true, key: "buyDate", width: "1px" },
        { title: "開始日", align: 'start', sortable: true, key: "startDate", width: "1px" },
        { title: "読了日", align: 'start', sortable: true, key: "endDate", width: "1px" },
        { title: "カテゴリー", align: 'start', sortable: true, key: "category", width: "100px" },
        { title: "ひとこと", align: 'start', sortable: true, key: "impression", width: "200px" }
      ];
      break;
    case "game":
      contents.value = gameList;
      headers.value = [
        { title: 'タイトル', align: 'start', sortable: true, key: 'title', width: '200px' },
        { title: '開発元', align: 'start', sortable: true, key: 'developer', width: '100px' },
        { title: '発売日', align: 'start', sortable: true, key: 'release_date', width: '100px' },
        { title: 'ジャンル', align: 'start', sortable: true, key: 'genre', width: '100px' },
        { title: '概要', align: 'start', sortable: true, key: 'summary', width: '200px' },
        { title: 'プレイ時間', align: 'start', sortable: true, key: 'play_time', width: '100px' },
        { title: '開始日', align: 'start', sortable: true, key: 'start_date', width: '100px' },
        { title: '終了日', align: 'start', sortable: true, key: 'end_date', width: '100px' },
        { title: 'ひとこと', align: 'start', sortable: true, key: 'impression', width: '200px' },
        { title: 'メモ', align: 'start', sortable: true, key: 'memo', width: '200px' }
      ];
      break;
    default:
      contents.value = entertainmentList;
  };
};
</script>

<template>
  <v-data-table
    class="pa-5"
    :headers="headers"
    :items="contents"
    item-value="name"
    density="compact"
    :fixed-header="true"
    :multi-sort="true"
    scrollX
  ></v-data-table>
</template>

<style>
/* vue3だとhide-default-footerが動いていないようなのでcssで無理やり消す */
.v-data-table-footer {
  display: none !important;
}

/* 横スクロールさせたい */
.v-data-table {
  /* white-space : nowrap; */
  font-size: 0.9rem !important;
}

.v-data-table tr {
  height: 60px !important;
}
</style>
