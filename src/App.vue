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
    <div class="data">
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
  </div>
</template>

<style scoped>
body {
  margin: 0;
  padding: 0;
}

#app {
  background-color: rgb(24, 145, 220);
  min-height: 150vh;
}

.data {
  display: flex;
  flex: 1;
}

.addData {
  padding: 50px;
  margin-left: 390px;
}

.addData button {
  border: 2px solid black;
  border-radius: 5px;
}

.addData input {
  width: 500px;
  height: 35px;
  margin-bottom: 10px;
  margin-right: 20px;
  border-radius: 10px;
  border: 2px solid black;
}
ul {
  list-style-type: none;
}

.completed {
  text-decoration: line-through;
}

.dataNotReady {
  margin-left: 100px;
  border-bottom: none;
}

.dataNotReady input {
  width: 30px;
  height: 13px;
}

.dataNotReady label {
  margin-bottom: 200px;
}

.allData {
  border: 2px solid black;
  padding: 20px;
  margin-left: 150px;
  margin-top: 20px;
  width: 500px;
  height: 400px;
  overflow-y: scroll;
  margin-left: 50px;
}

.allData p {
  text-align: center;
  margin-bottom: 50px;
  font-size: 30px;
}

.allData button {
  margin-left: 20px;
  background-color: red;
}
</style>
