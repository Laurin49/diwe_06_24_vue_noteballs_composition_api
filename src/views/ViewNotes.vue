<template>
  <div class="notes">
    <div class="card has-background-grey-dark p-4 mb-5">
      <div class="field">
        <div class="control">
          <textarea v-model="newNote" 
          ref="newNoteRef"
          class="textarea" 
          placeholder="Add a new note" />
        </div>
      </div>
      
      <div class="field is-grouped is-grouped-right">
        <div class="control">
          <button 
            @click="addNote"
            class="button is-link has-background-success"
            :disabled="!newNote">
            New Note
          </button>
        </div>
      </div>
    </div>
    
    <Note 
      v-for="note in notes" 
      :key="note.id" 
      :note="note"
      @delete-clicked="deleteNote"></Note>
    
  </div>
</template>
<script setup>
/* imports */
import { ref } from 'vue';
import Note from '@/components/Notes/Note.vue'

/* notes */
  const newNote = ref('')
  const newNoteRef = ref(null)
  const notes = ref([
    {
      id: 'id1',
      content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Quae, nemo laudantium porro distinctio a, ea autem quo, illum voluptates sapiente tenetur quod aperiam odio. Tempora odio illum dolorem incidunt ullam?'
    },
    {
      id: 'id2',
      content: 'Beintraing: Kniebeugen, Beinstrecker, Beincurls, Wadenheben'
    },
    {
      id: 'id3',
      content: 'Rückentraining: Klimmzüge, Rudern vorgebeugt L.H., Rudern Expander, Nackenziehen'
    }
  ])
  const addNote = () => {
    let currentDate = new Date().getTime(),
        id = currentDate.toString

    let note = {
      id: id,
      content: newNote.value
    }
    notes.value.unshift(note)
    newNote.value = ''
    newNoteRef.value.focus()
  }
  const deleteNote = (idToDelete) => {
    notes.value = notes.value.filter(note => {return note.id !== idToDelete})
  }
</script>
<style scoped>
</style>