<script setup lang="ts">
import { ref, onMounted } from 'vue';
import axios from 'axios';

axios.defaults.baseURL = 'http://localhost:4000';

let list = ref<string[]>([]);
const inputValue = ref('');

const addItem = async () => {
  const { data } = await axios.post('/items', { item: inputValue.value });

  list.value = [...list.value, data];
};

onMounted(async () => {
  const { data } = await axios.get('/items');

  list.value = data;
});
</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>

  <div>
    <input class="input" type="text" v-model="inputValue" />

    <button class="button" @click="addItem">Add value</button>

    <ul>
      <li v-for="item of list" :key="item">{{ item }}</li>
    </ul>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}

.input {
  display: block;
  min-width: 200px;
  min-height: 30px;
  margin-bottom: 20px;
  border-radius: 6px;
}

.button {
  cursor: pointer;
  min-width: 200px;
  min-height: 30px;
  margin-bottom: 20px;
  border-radius: 6px;
}
</style>
