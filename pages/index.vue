<template>
    <div class="homepage-container">
        <h1>🏠 Homepage</h1>
        <NuxtLink class="fancy-link" to="/users-api">🔗 Lista de usuarios API</NuxtLink>
        <br>
        <NuxtLink class="fancy-link" to="/users-json">📄 Lista de usuarios JSON</NuxtLink>
        <br>
        <NuxtLink class="fancy-link" to="/users-local">⤵️ Lista de usuarios Local</NuxtLink>
        <br>
        <NuxtLink class="fancy-link" to="/nasa-api">🪐 Nasa API</NuxtLink>
    </div>
</template>

<script setup>
</script>

<style scoped>
.homepage-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, #f8fafc 0%, #e0e7ef 100%);
  font-family: 'Inter', 'Segoe UI', Arial, sans-serif;
}

h1 {
  color: #22223b;
  font-size: 2.5rem;
  margin-bottom: 2rem;
  letter-spacing: 2px;
  text-shadow: 0 2px 8px #e0e7ef;
}

.fancy-link {
  display: inline-block;
  margin: 0.5rem 0;
  padding: 0.75rem 2rem;
  border-radius: 2rem;
  background: #fff;
  color: #3a86ff;
  font-weight: 600;
  font-size: 1.1rem;
  text-decoration: none;
  box-shadow: 0 2px 12px 0 rgba(58,134,255,0.08);
  transition: background 0.2s, color 0.2s, box-shadow 0.2s, transform 0.1s;
}

.fancy-link:hover {
  background: #3a86ff;
  color: #fff;
  box-shadow: 0 4px 24px 0 rgba(58,134,255,0.18);
  transform: translateY(-2px) scale(1.04);
}
</style>