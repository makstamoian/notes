<script setup>
    const props = defineProps({
        disabled: Boolean,
    })
    defineEmits(["click"])
</script>

<template>
    <button :disabled="props.disabled" @click="$emit('click')">
        <slot></slot>
    </button>
</template>

<style scoped>
    button {
        background-color: #3e6ae1;
        color: whitesmoke;
        padding: 12px;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-family: inherit;
        font-weight: 600;
    }

    button:disabled {
        opacity: 0.8;
        cursor: not-allowed;
    }
</style>