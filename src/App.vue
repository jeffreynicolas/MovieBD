<script setup>
</script>

<template>
  <header>
    <h1>J.A. Movies</h1>
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/filmes">Filmes</router-link>
      <router-link to="/tv">Programas de TV</router-link>
    </nav>
  </header>
  <main>
    <router-view />
  </main>
</template>


<style scoped>
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  padding: 1rem 2rem;
  background-color: #1a1a1a; 
  border-bottom: 2px solid #444; 
}

nav a {
  text-decoration: none;
  color: #fff;
  font-weight: bold;
  padding-left: 4rem;
  transition: color 0.3s ease; 
}

nav a:hover {
  color: #ff9900; 
}


header {
  height: 3rem;
  display: flex;
  align-items: center;
  background-color: #1a1a1a;
  color: #fff;
  font-size: 1.2rem;
  padding-left: 3rem;
}
h1 {
  
  color: #fff;
  
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.8), 0 0 20px rgba(255, 255, 255, 0.8), 0 0 30px rgba(255, 255, 255, 0.8), 0 0 40px #0ff, 0 0 70px #0ff, 0 0 80px #0ff, 0 0 100px #0ff;
  transition: text-shadow 0.5s ease-in-out;
}

h1:hover {
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.8), 0 0 20px rgba(255, 255, 255, 0.8), 0 0 30px rgba(255, 255, 255, 0.8), 0 0 40px #f06, 0 0 70px #f06, 0 0 80px #f06, 0 0 100px #f06;
}

</style>
