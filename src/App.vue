<script setup>
import { ref, computed } from "vue";

const activity = ref("");

const data = ref([]);

const dataIncomplete = ref(false);

const addData = () => {
  data.value.push({ text: activity.value, done: false });
  activity.value = "";
};

const filterData = computed(() => {
  return dataIncomplete.value ? data.value.filter((todo) => !todo.done) : data.value;
});

const removeData = (index) => {
  data.value.splice(index, 1);
};
</script>

<template>
  <div id="app">
    <div class="addData">
      <input v-model="activity" placeholder="Tambahkan Kegiatan" />
      <button @click="addData">Submit</button>
    </div>

    <div class="dataNotReady">
      <label>
        <input type="checkbox" v-model="dataIncomplete" />
        Tampilkan kegiatan yang belum selesai
      </label>
    </div>

    <div class="allData">
      <p>Daftar Kegiatan</p>
      <ul>
        <li v-for="(todo, index) in filterData" :key="index">
          <input type="checkbox" v-model="todo.done" />
          <span :class="{ completed: todo.done }">{{ todo.text }}</span>
          <button @click="removeData(index)">Hapus</button>
        </li>
      </ul>
    </div>
    
  </div>
</template>

<style scoped></style>
