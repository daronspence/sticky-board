<template>
  <div id="app">
    <board>
      <note v-for="note in notes" :note="note" :key="note.id"></note>
    </board>
    <button @click="addNote" class="absolute top-0 left-0 px-2 py-1 ml-4 mt-4 bg-blue-600 text-white rounded uppercase text-sm shadow-lg border hover:bg-blue-700">Add Note</button>
    <note-selector :notes="notes"></note-selector>
  </div>
</template>

<script>
import Board from './components/Board.vue'
import Note from './components/Note.vue'
import NoteSelector from './components/NoteSelector.vue'

export default {
  name: 'app',
  components: {
    Board,
    Note,
    NoteSelector
  },
  data() {
    return {
      notes: [
        {
          id: 1,
          body: 'lorem ipsum',
          xpos: 55.26,
          ypos: 8.5
        },
        {
          id: 2,
          body: 'some note text here',
          xpos: 12,
          ypos: 63
        }
      ]
    }
  },
  methods: {
    addNote() {
      this.notes.push({
        id: (new Date).toString(),
        xpos: 5,
        ypos: 5,
        body: '',
      })
    }
  }
}
</script>

<style>
#app {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  position: relative;
  min-width: 800px;
  min-height: 500px;
  display: flex;
}

.moveable-control-box {
  display: none !important;
}
</style>
