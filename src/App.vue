<script setup>
import { reactive } from 'vue'
import { v4 as uuidv4 } from 'uuid'

import Button from './components/UI/Button.vue';
import Note from './components/Note.vue'

const state = reactive({ 
  note: { title: "", value: "" }, 
  notes: JSON.parse(localStorage.getItem("notes")) ?? [],
});

function addNote() {
  if(state.note.value.trim() !== "") {
    let note = {title: state.note.title.trim(), value: state.note.value.trim(), id: uuidv4()}
    state.notes.unshift(note)
    localStorage.setItem("notes", JSON.stringify(state.notes))
    state.note.value = ""
    state.note.title = ""
  }

}

function deleteNote(id) {
  state.notes = state.notes.filter((note) => note.id !== id);
  localStorage.setItem("notes", JSON.stringify(state.notes));
}

</script>

<template>
  <div class="newNoteForm">
    <input type="text" v-model="state.note.title" class="titleInput" placeholder="Title..."/>
    <textarea type="text" v-model="state.note.value" rows="5" cols="70" class="valueInput" placeholder="Note..."/>
    <Button 
      @click="addNote" 
      :disabled="state.note.value === ''">
        Save note
    </Button>
  </div>
  <div class="notes">
    <Note v-for="note in state.notes"
      :note="note"
      @delete="deleteNote">
    </Note>
  </div>
</template>

<style scoped>
.notes {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  gap: 16px;
  margin-top: 32px;
}

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
