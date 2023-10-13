<script setup>
import { ref, computed, watch } from 'vue';

const users = ref([
  { id: 1, name: "Nasir" },
  { id: 2, name: "Basir" },
  { id: 3, name: "Jahir" },
  { id: 4, name: "Karim" },
  { id: 5, name: "Rahim" },
  { id: 6, name: "Billal" },
  { id: 7, name: "Momin" }
]);

const searchQuery = ref('');

const filteredUsers = computed(() => {
  const query = searchQuery.value.toLowerCase();
  if (!query) {
    return users.value; 
  }
  return users.value.filter(user => user.name.toLowerCase().includes(query));
});

watch(searchQuery, (newVal, oldVal) => {
  console.log(`Search query changed from "${oldVal}" to "${newVal}"`);
});
</script>
<template>
  <div>
    <input v-model="searchQuery" placeholder="Search users" />
    <ul>
      <li v-for="user in filteredUsers" :key="user.id">{{ user.name }}</li>
    </ul>
  </div>
</template>
