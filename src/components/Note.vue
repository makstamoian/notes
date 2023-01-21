<script setup>
const props = defineProps({
    note: {
        type: Object,
        required: true
    }
})

defineEmits(["delete"])
</script>

<template>
    <div class="note">
        <h3 class="title">{{ props.note.title }}</h3>
        <span>
        {{ props.note.value }}
        </span>
        <button @click="$emit('delete', props.note.id)" class="deleteButton" title="Delete note">×</button>
    </div>
</template>

<style scoped>
.note {
    padding: 16px;
    border: 1px solid rgb(161, 192, 250);
    border-radius: 4px;
    background-color: rgb(241, 246, 253);
    white-space: pre-wrap;
    position: relative;
}

.title {
  margin: 0 0 8px 0;
}

.deleteButton {
    border: none;
    background-color: transparent;
    border-radius: 4px;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 20px;
    height: 20px;
    color: rgb(161, 192, 250);
    cursor: pointer;
    position: absolute;
    top: 8px;
    right: 8px;
    font-size: 16px;
}

.deleteButton:hover {
    background-color: rgb(204, 219, 253);
    color: red;
}

</style>