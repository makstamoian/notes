<script setup>
import { reactive } from 'vue'

import Note from './components/Note.vue';
import AddNoteForm from './components/AddNoteForm.vue'

const state = reactive({
  notes: JSON.parse(localStorage.getItem("notes")) ?? [],
});

function addNote(note) {
  state.notes.unshift(note);

  localStorage.setItem("notes", JSON.stringify(state.notes));
}

function deleteNote(id) {
  state.notes = state.notes.filter((note) => note.id !== id);

  localStorage.setItem("notes", JSON.stringify(state.notes));
}

</script>

<template>
  <AddNoteForm @addNote="addNote" />

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
</style>
