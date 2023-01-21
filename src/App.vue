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
    <input type="text" v-model="state.note.title" class="titleInput"/>
    <textarea type="text" v-model="state.note.value" v-on:keypress="addNote" rows="5" cols="70" class="valueInput"/>
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
  border: 1px solid cornflowerblue;
  border-radius: 8px;
  background-color: rgb(223, 234, 248);
  box-shadow: 1px 1px 3px 1px rgb(135, 187, 255);
}

.title {
  margin: 0 0 8px 0;
}

.titleInput {

}

.newNoteForm {
  display: flex;
  flex-direction: column;
  max-width: 600px;
  gap: 16px;
  margin: 0 auto;
}

</style>
