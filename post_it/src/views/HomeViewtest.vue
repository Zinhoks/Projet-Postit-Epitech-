<template>

    <div class="app">
      <h1>Notes</h1> <button v-on:click="createNote" class="create-new-button">Create new</button>
      <div class="notes">
        <nav>
          <p v-if="!notes.length">No notes saved</p>
          <ul v-if="notes.length">
            <li v-for="note in notes">
              <button v-on:click="currentNote = note" :class="{active: note === currentNote}">{{note.title}}</button>
            </li>
          </ul>
        </nav>
        <div v-if="currentNote" class="current-note">
          <input v-model="currentNote.title" ref="noteTitle">
          <textarea v-model="currentNote.contents"></textarea>
        </div>
      </div>
    </div>
    
    </template>
    
    <style>
    
    body {
      padding: 20px 30px;
    }
    h1 {
      display: inline-block;
      margin-right: 20px;
    }
    .create-new-button {
      position: relative;
      top: -10px;
    }
    nav ul {
      list-style-type: none;
    }
    nav button, nav button:hover, nav button:active, nav button:focus {
      background: none;
      color: #606c76;
    }
    nav button {
      display: block;
      width: 100%;
      border: none;
      padding: 0 10px;
      font-size: 18px;
      font-weight: normal;
      text-transform: none;
      text-align: left;
    }
    nav button:hover {
      text-decoration: underline;
    }
    nav button.active {
      background: gray;
      color: white;
    }
    .notes {
      display: flex;
    }
    nav {
      flex: 0 0 calc(33% - 20px);
      margin-right: 20px;
    }
    .current-note {
      flex: 1;
    }
    .current-note input, .current-note textarea {
      color: #606c76;
      border: none;
      border-radius: 0;
      padding: 5px;
    }
    .current-note input:hover, .current-note textarea:hover,
    .current-note input:focus, .current-note textarea:focus {
      background: lavender;
    }
    .current-note input {
      font-size: 3.6rem;
      line-height: 1.25;
      font-weight: 300;
      letter-spacing: -.1rem;
      margin-bottom: 2.0rem;
      margin-top: 0;
    }
    .current-note textarea {
      font-size: 18px;
      color: #606c76;
    }
    
    </style>


<script>

const app = new Vue({
    el: '.app',
    data: {
      notes: [],
      currentNote: null
    },
    mounted() {
      if (localStorage.notes) {
        this.notes = JSON.parse(localStorage.notes);
      }
    },
    watch: {
      notes: {
        handler(newNotes) {
          localStorage.notes = JSON.stringify(newNotes);
        },
        deep: true
      }
    },
    methods: {
      createNote() {
        const newNote = {title: '', contents: ''};
        this.notes.push(newNote);
        this.currentNote = newNote;
        this.$nextTick(function() {
          this.$refs.noteTitle.focus();      
        });
    }
}
});
</script>