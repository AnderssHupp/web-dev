<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  options: {
    type: Array,
    required: true,
  },
  modelValue: {
    type: Array,
    default: () => [],
  },
  value: {
    type: Array,
    default: () => [],
  },
});

const emit = defineEmits(["update:modelValue", "update:value", "change"]);

const selectedValues = ref([]);

function syncFromProps() {
  const source = props.modelValue.length ? props.modelValue : props.value;
  selectedValues.value = Array.isArray(source) ? [...source] : [];
}

function isChecked(option) {
  return selectedValues.value.includes(option);
}

function handleChange(option, event) {
  const { checked } = event.target;

  if (checked && !selectedValues.value.includes(option)) {
    selectedValues.value = [...selectedValues.value, option];
  } else if (!checked) {
    selectedValues.value = selectedValues.value.filter(
      (selectedOption) => selectedOption !== option,
    );
  }

  emit("update:modelValue", selectedValues.value);
  emit("update:value", selectedValues.value);
  emit("change", selectedValues.value);
}

watch(
  () => [props.modelValue, props.value],
  () => {
    syncFromProps();
  },
  { immediate: true, deep: true },
);
</script>

<template>
  <div class="checkbox-group">
    <div
      v-for="(option, index) in options"
      :key="`${option}-${index}`"
      class="checkbox-item"
    >
      <input
        type="checkbox"
        :id="`option-${index}`"
        class="checkbox-input"
        :checked="isChecked(option)"
        @change="handleChange(option, $event)"
      />
      <label
        :for="`option-${index}`"
        :class="{ 'label-active': isChecked(option) }"
      >
        {{ option }}
      </label>
    </div>
  </div>
</template>

<style scoped>
.checkbox-group {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.checkbox-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.checkbox-input {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: 1px solid #0b1b3b;
  cursor: pointer;
  accent-color: #02ade6;
}

.checkbox-item label {
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  color: #0b1b3b;
}

.checkbox-item .label-active {
  font-weight: 700;
}
</style>
