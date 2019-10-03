<template>
  <div id="note-selector" class="p-4 bg-gray-200 border-l-2">
      <ul>
          <li v-for="note in notes" :key="note.id" @mouseenter="highlightNote(note.id)" @mouseleave="unHighlightNote(note.id)">{{ note.body }}</li>
      </ul>
  </div>
</template>

<script>
export default {
    props: ['notes'],
    methods: {
        highlightNote(id) {
            const note = document.querySelector('#note-'+id);
            note.classList.add('hovered')
        },
        unHighlightNote(id) {
            const note = document.querySelector('#note-'+id);
            note.classList.remove('hovered')
        }
    }
}
</script>

<style>
    #note-selector {
        height: 100vh;
        width: 200px;
    }
</style>