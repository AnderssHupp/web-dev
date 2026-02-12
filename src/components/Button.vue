<script setup>
const props = defineProps({
  type: {
    type: String,
    default: "button",
  },
});
</script>

<template>
  <button :type="props.type">
    <slot></slot>
  </button>
</template>

<style scoped>
button {
  background-color: #ffffff;
  height: 48px;
  width: 100%;
  max-width: 250px;
  padding: 0 1.5rem;
  border-radius: 1.5rem;
  border: none;
  cursor: pointer;
  transition: all 0.2s ease;
}
button:hover {
  opacity: 0.9;
}

@media (max-width: 768px) {
  button {
    max-width: none;
  }
}
</style>
