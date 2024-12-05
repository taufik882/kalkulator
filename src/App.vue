<template>
  <div id="app">
    <header>
      <h1>Kalkulator Persentase</h1>
      <nav>
        <button :class="{ active: currentFeature === 'percentageChange' }" 
                @click="currentFeature = 'percentageChange'">Perubahan Persentase</button>
        <button :class="{ active: currentFeature === 'percentageOfTotal' }" 
                @click="currentFeature = 'percentageOfTotal'">Persentase Jumlah</button>
      </nav>
    </header>
    <main>
      <PercentageChange v-if="currentFeature === 'percentageChange'" />
      <PercentageOfTotal v-else />
    </main>
    <footer>
      <p>&copy; 2024 Kalkulator Persentase</p>
    </footer>
  </div>
</template>

<script>
import PercentageChange from './components/PercentageChange.vue';
import PercentageOfTotal from './components/PercentageOfTotal.vue';

export default {
  components: { PercentageChange, PercentageOfTotal },
  data() {
    return {
      currentFeature: 'percentageChange',
    };
  },
};
</script>

<style>
/* Global Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Base Styles */
body {
  font-family: 'Roboto', Arial, sans-serif;
  background-color: #f5f7fa;
  color: #333;
}

#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

/* Header Styles */
header {
  background-color: #007bff;
  color: white;
  padding: 20px;
  text-align: center;
  border-radius: 8px;
  margin-bottom: 20px;
}

header h1 {
  font-size: 1.8rem;
  margin-bottom: 10px;
}

nav {
  display: flex;
  justify-content: center;
  gap: 10px;
}

nav button {
  background-color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 5px;
  cursor: pointer;
  color: #007bff;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

nav button.active {
  background-color: #0056b3;
  color: white;
}

nav button:hover {
  background-color: #e2e6ea;
}

/* Main Styles */
main {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}

/* Footer Styles */
footer {
  text-align: center;
  color: #777;
  font-size: 0.9rem;
}

/* Responsiveness */
@media (max-width: 600px) {
  header h1 {
    font-size: 1.4rem;
  }

  nav button {
    font-size: 0.9rem;
    padding: 8px 10px;
  }
}
</style>
