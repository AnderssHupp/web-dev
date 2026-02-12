<script setup>
import { ref } from "vue";

const items = ["Lorem Ipsum", "Utilizador", "Quantum solum", "Marcus Tremer"];
const activeIndex = ref(1);

function setActive(index) {
  activeIndex.value = index;
}
</script>

<template>
  <aside class="sidebar">
    <nav class="nav">
      <ul class="info-list">
        <li
          v-for="(item, index) in items"
          :key="item"
          :class="{ 'item-active': activeIndex === index }"
          @click="setActive(index)"
        >
          {{ item }}
        </li>
      </ul>
    </nav>
    <footer class="sidebar-footer">
      <p class="footer-content">2019® Premium-minds.com</p>
    </footer>
  </aside>
</template>

<style scoped>
.sidebar {
  width: 300px;
  display: flex;
  flex-direction: column;
  background-color: #343f53;
  color: #ffffff;
}

nav {
  flex: 1;
  padding: 3rem 2.5rem;
}

.info-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  padding: 0;
  margin: 0;
}

.info-list li {
  font-size: 1rem;
  cursor: pointer;
  padding: 0.35rem 0.5rem;
  border-radius: 0.25rem;
  font-weight: 400;
}

.info-list li:hover {
  opacity: 0.9;
}

.info-list li.item-active {
  font-weight: 600;
}

.sidebar-footer {
  background-color: #263142;
  border-top: 2px solid #434b5d;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.footer-content {
  font-size: 0.8rem;
  color: #ffffff;
  text-align: center;
}

@media (max-width: 1024px) {
  .sidebar {
    width: 240px;
  }

  nav {
    padding: 2rem 1.25rem;
  }
}

@media (max-width: 768px) {
  .sidebar {
    width: 100%;
  }

  nav {
    padding: 1rem;
  }

  .info-list {
    flex-direction: row;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .info-list li {
    background-color: rgba(255, 255, 255, 0.08);
    font-size: 0.9rem;
  }

  .sidebar-footer {
    height: 48px;
  }

  .footer-content {
    font-size: 0.72rem;
  }
}
</style>
