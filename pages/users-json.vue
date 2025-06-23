<script setup>
    const { data: users, error } = await useFetch('/users.json');
</script>

<template>
    <div class="users-list-container">
        <h1>Usuarios de JSON local</h1>
        <ul>
            <li v-for="user in users" :key="user.id">{{ user.name }} - {{ user.email }}</li>
        </ul>
        <p v-if="error" class="error-msg">Error: {{ error.message }}</p>
    </div>
</template>

<style scoped>
.users-list-container {
  max-width: 500px;
  margin: 2rem auto;
  background: #fff;
  border-radius: 1.5rem;
  box-shadow: 0 2px 16px 0 rgba(58,134,255,0.08);
  padding: 2rem 2.5rem;
  font-family: 'Inter', 'Segoe UI', Arial, sans-serif;
}

h1 {
  color: #3a86ff;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  text-align: center;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  padding: 0.75rem 0;
  border-bottom: 1px solid #e0e7ef;
  font-size: 1.1rem;
  color: #22223b;
}
li:last-child {
  border-bottom: none;
}
.error-msg {
  color: #e63946;
  margin-top: 1.5rem;
  text-align: center;
}
</style>