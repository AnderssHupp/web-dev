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
      <input
        :type="type"
        :name="name"
        :id="id"
        v-model="modelValue"
        class="input"
        @blur="handleBlur"
        @input="handleInput"
      />
      <span v-if="error" class="error-message">{{ error }}</span>
    </div>
  </div>
</template>

<style scoped>
.input-container {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.input-container label {
  font-size: 0.875rem;
  font-weight: 600;
  color: #7f8fa4;
}

.input {
  width: 100%;
  border: none;
  border-bottom: 2px solid #cecece;
  padding: 0.5rem 0.75rem;
  font-size: 0.95rem;
  background: transparent;
  transition: border-color 0.2s ease;
}

.input:focus {
  outline: none;
  border-bottom: 2px solid #02ade6;
  border-bottom: 2px solid #cecece;
}

.input-wrapper {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.error-message {
  color: #ef4444;
  font-size: 0.8rem;
  font-weight: 500;
}
</style>
