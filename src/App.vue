<script setup>
import { ref, computed } from "vue";

const activity = ref("");

const data = ref([]);

</script>

<template>
  <div id="app">    
    <div class="addData">
      <input v-model="activity" placeholder="Tambahkan Kegiatan" />
      <button @click="addData">Submit</button>
    </div>
  </div>
</template>

<style scoped>

</style>
