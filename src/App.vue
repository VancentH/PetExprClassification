<script setup lang="ts">
import MainContent from "./components/MainContent.vue";
import MainNav from "./components/MainNav.vue";
import HistoryList from "./components/HistoryList.vue";
</script>

<template>
  <header>
    <MainNav></MainNav>
  </header>

  <main>
    <MainContent></MainContent>
    <!-- <HistoryList></HistoryList> -->
  </main>
</template>

<style scoped></style>
