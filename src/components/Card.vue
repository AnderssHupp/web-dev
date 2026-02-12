<script setup>
import { ref } from "vue";
const isOpen = ref(true);
const props = defineProps({
  title: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="card">
    <div class="card-header">
      <h2>{{ title }}</h2>
      <button type="button" @click="isOpen = !isOpen">
        {{ isOpen ? "−" : "+" }}
      </button>
    </div>
    <div class="card-content" v-if="isOpen">
      <slot></slot>
    </div>
  </div>
</template>

<style scoped>
.card {
  background-color: #ffffff;
  border-radius: 6px;
  margin-bottom: 0px;
  overflow: hidden;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.04);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #4141412c;
  padding: 0rem 1.5rem;
  border-bottom: 1px solid #e5e7eb;
}

.card-header h2 {
  font-size: 1.2rem;
  font-weight: 600;
  color: #0b1b3b;
}

.card-content {
  padding: 2.5rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 32px;
}

button {
  background: none;
  border: none;
  font-size: 2.5rem;
  font-weight: bold;
  color: #6b7280;
  cursor: pointer;
}
</style>
