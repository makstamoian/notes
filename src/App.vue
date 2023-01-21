<script setup>
import { reactive } from 'vue'

const state = reactive({ note:{title: "", value: ""}, notes: JSON.parse(localStorage.getItem("notes")) ?? []})

function addNote(event){
  if(event.key === "Enter" && state.note.value.trim() !== ""){
    event.preventDefault()
    let note = {...state.note}
    state.notes.push(note)
    localStorage.setItem("notes", JSON.stringify(state.notes))
    state.note.value = ""
    state.note.title = ""

  }
}

</script>

<template>
  <div class="newNoteForm">
    <input type="text" v-model="state.note.title" class="titleInput" placeholder="Title..."/>
    <textarea type="text" v-model="state.note.value" v-on:keypress="addNote" rows="5" cols="70" class="valueInput" placeholder="Note..."/>
  </div>
  <div class="notes">
    <div v-for="note in state.notes" class="note">
      <h3 class="title">{{ note.title }}</h3>
      {{ note.value }}

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
