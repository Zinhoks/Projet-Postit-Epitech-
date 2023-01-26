
<template>

  <div class="post-it">
    <textarea placeholder="Write a note" name="note"  v-model="note" id="note" cols="25" rows="8"></textarea>
    <RouterLink to="/">Voir plus</RouterLink>
  </div>


</template>

<script>
export default {
  name: "note",
  
  data() {
    return {
      note: '',
      array: [],
    }
  },

  mounted() {
    if (localStorage.note) {
      this.note = JSON.parse(localStorage.note);
    }
  },
props: ["notes"],
  watch: {
    note: {
      handler (newNote) {
        localStorage.note= JSON.stringify(newNote);
    },
    deep: true,
  }

}
}



</script>
  
 
  




































<style>
body {
  text-align: center;
  margin-top: 2em;
}

.post-it,
.post-it textarea {
  border: 0;
  padding: 4px;
  font-size: 1.5em;
  font-family: "Mistral", cursive;
  /* Comic Sans for Windows :p*/
  color: #1536bd;
}

.post-it textarea {
  background: transparent;
  padding: 10px;
  width: 300px;
  height: 250px;
}

.post-it {
  position: relative;
  display: inline-block;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, .2);
  background-color: #F8E57C;
  background-image: linear-gradient(to bottom right, #f8e072, #f5f593);
}

.post-it:after {
  content: " ";
  position: absolute;
  right: 5px;
  top: 75%;
  bottom: 2%;
  width: 50%;
  z-index: -10;
  box-shadow: -7px 4px 15px rgba(0, 0, 0, .5);
  transform: rotate(3deg);
}
</style>

