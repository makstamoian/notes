<script setup>
import { reactive } from 'vue'

const state = reactive({ note:{title: "", value: ""}, notes: JSON.parse(localStorage.getItem("notes")) ?? []})

function addNote(event){
  if(state.note.value.trim() !== ""){
    event.preventDefault()
    let note = {title: state.note.title.trim(), value: state.note.value.trim()}
    state.notes.unshift(note)
    localStorage.setItem("notes", JSON.stringify(state.notes))
    state.note.value = ""
    state.note.title = ""
  }

}

</script>

<template>
  <div class="newNoteForm">
    <input type="text" v-model="state.note.title" class="titleInput" placeholder="Title..."/>
    <textarea type="text" v-model="state.note.value" rows="5" cols="70" class="valueInput" placeholder="Note..."/>
    <button @click="addNote" :disabled="state.note.value === ''">Save note</button>
  </div>
  <div class="notes">
    <div v-for="note in state.notes" class="note">
      <h3 class="title">{{ note.title }}</h3>
      <span>
      {{ note.value }}
      </span>
    </div>
  </div>
</template>

<style scoped>
.notes {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  gap: 16px;
  margin-top: 32px;
}

.note {
  padding: 16px;
  border: 1px solid rgb(161, 192, 250);
  border-radius: 4px;
  background-color: rgb(241, 246, 253);
  white-space: pre-wrap;
}

.title {
  margin: 0 0 8px 0;
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
