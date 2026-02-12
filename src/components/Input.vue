<script setup>
const props = defineProps({
  type: {
    type: String,
    required: true,
  },
  label: {
    type: String,
    required: true,
  },
  name: {
    required: true,
  },
  id: {
    type: String,
    required: true,
  },
  prefix: {
    type: String,
    required: false,
  },
  error: {
    type: String,
    required: false,
  },
});

const modelValue = defineModel();
const emit = defineEmits(["blur", "input"]);

function handleBlur(event) {
  emit("blur", event);
}

function handleInput(event) {
  emit("input", event);
}
</script>

<template>
  <div class="input-container">
    <label :for="id">{{ label }}</label>
    <div class="input-wrapper">
      <span v-if="prefix">{{ prefix }}</span>
      <input
        :type="type"
        :name="name"
        :id="id"
        v-model="modelValue"
        class="input"
        @blur="handleBlur"
        @input="handleInput"
      />
    </div>
  </div>
  <p v-if="error" class="error-message">{{ error }}</p>
</template>

<style scoped>
.input-container {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.input-container label {
  font-size: 0.8rem;
  font-weight: 600;
  color: #6b7280;
}

.input {
  width: 100%;
  border: none;
  border-bottom: 1px solid #d1d5db;
  padding: 0.5rem 0;
  font-size: 0.95rem;
  background: transparent;
  transition: border-color 0.2s ease;
}

.input:focus {
  outline: none;
  border-bottom: 2px solid #1da1c9;
  border-bottom: 2px solid #bdbdbdef;
}

.input-wrapper {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.error-message {
  color: #ef4444;
  font-size: 0.8rem;
  font-weight: 500;
}
</style>
