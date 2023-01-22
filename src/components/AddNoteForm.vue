<script setup>
    import { ref } from 'vue';
    import { v4 as uuidv4 } from 'uuid';

    import Button from './UI/Button.vue';

    const emit = defineEmits(["addNote"]);

    const title = ref("");
    const text = ref("");

    const addNote = () => {
      if (text.value.trim() === "") {
        return;
      }

      const note = {
        id: uuidv4(),
        title: title.value.trim(), 
        value: text.value.trim(),
      };

      emit('addNote', note);

      title.value = "";
      text.value = "";
    }

</script>

<template>
    <div class="newNoteForm">
        <input type="text" v-model="title" class="titleInput" placeholder="Title..." />
        <textarea type="text" v-model="text" rows="5" cols="70" class="valueInput" placeholder="Note..." />
        <Button @click="addNote" :disabled="text === ''">
                Save note
        </Button>
    </div>
</template>

<style scoped>
.newNoteForm {
  display: flex;
  flex-direction: column;
  max-width: 600px;
  gap: 16px;
  margin: 0 auto;
  align-items: flex-start;
}

input, textarea {
  background-color: #f4f4f4;
  border: none;
  padding: 12px;
  border-radius: 4px;
  outline: none; 
  border: 1px solid transparent;
  font-family: inherit;
  
}

input:focus, textarea:focus{
  border-color: #d0d1d2;
}

textarea {
  resize: none;
}
</style>