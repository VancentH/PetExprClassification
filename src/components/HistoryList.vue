<template>
  <div>
    <div class="border-2">
      <div v-for="(item, index) in list" :key="index" class="item relative inline-block">
        <img src="" alt="pet image" class="h-48 w-48 rounded-md object-cover">
        <div class="absolute top-0 h-full w-full bg-black rounded-md bg-opacity-25 flex items-center justify-center">
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
// api get filename
import { reactive } from "vue";

export default {
  setup() {
    const list = reactive([
      {
        filename: 'img1.jpg'
      },
      {
        filename: 'img2.jpg'
      },
      {
        filename: 'img2.jpg'
      },
      {
        filename: 'img2.jpg'
      },
      {
        filename: 'img2.jpg'
      },
      {
        filename: 'img2.jpg'
      },
    ])

    return {
      list
    }
  }
}

</script>

<style></style>
