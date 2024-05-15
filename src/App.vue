<template>
  <div>
    <div>
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Tambah tugas" />
      <button @click="addTask">Tambah</button>
    </div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <input type="checkbox" v-model="task.completed" />
        <span :class="{ completed: task.completed }">{{ task.title }}</span>
        <button @click="deleteTask(index)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const tasks = ref([
  { title: 'Belajar Vue', completed: false },
  { title: 'Makan siang', completed: true },
  { title: 'Beli bahan makanan', completed: false }
]);

const newTask = ref('');

const addTask = () => {
  if (newTask.value.trim() === '') return;
  tasks.value.push({ title: newTask.value, completed: false });
  newTask.value = '';
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
