<script>
import Note from "../components/Note.vue";

export default{
    name: "HomeView",
    data() {
        return {
            count: 0,
            name: "zinho",
            array: [],
        };
    },
    methods: {
        plus() {
          // console.log("coucou")
            this.count = this.count + 1;
            this.array.push(this.count);
            // console.log(this.array)
            localStorage.setItem("array", JSON.stringify(this.array));

        }
        
    },
    
    components: { Note }
}


</script>

<template>
  <main>
    <button v-on:click="plus">ajouter un postit</button>
    {{element}}
    <div v-for="element in array" :key="element.id">
      <Note :key="element.id" :note="element.note"></Note>
    </div>
    

  </main>
</template>
