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
    width: 100%;
    max-width: 250px;
    padding: 0.5rem 1rem;
    border-radius: 1.5rem;
    border: none;
    cursor: pointer;
}

@media (max-width: 768px) {
    button {
        max-width: none;
    }
}
</style>