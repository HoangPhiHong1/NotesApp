<script setup>
import {ref} from "vue";
const showModal = ref(false)
const newNote = ref("")
const notes = ref([]);
const errorMessage = ref("")

function getRandomColor(){
  return "hsl("+ Math.random() * 360 +", 100%, 75%)";
}

const addNote = () =>{
  if (newNote.value.length<=10) {
    return errorMessage.value = "Notes need 10 characters minimum!"
  }
  notes.value.push({
    text: newNote.value,
    date: new Date(),
    id: Math.floor(Math.random() * 10000),
    backgroundColor: getRandomColor()
  })
  showModal.value = false
  newNote.value = ""
}
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal=false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal=true">+</button>
      </header>
      <div class="cards-container">
        <div 
        v-for="note in notes" 
        :key = "note.id"
        class ="card" 
        :style ="{backgroundColor: note.backgroundColor}"
        >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
        
      </div>
    </div>
  </main>
</template>

<style scoped> 
  @import url('https://fonts.googleapis.com/css2?family=Satisfy&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Serif&display=swap');

  main{
    width: 100vw;
    height: 100vh;
  }
  .container{
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }
  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-family: 'Satisfy', cursive;
    color: #FEBE98;
    font-weight: bold;
    font-size: 50vh;
  }
  h1{
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }
  header button{
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21, 20, 20);
    border-radius: 100%;
    color: white;
    font-size: 20px;
  }
  .card{
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding : 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .date{
    font-size: 12.5px;
    font-weight: bold;
    font-family: 'IBM Plex Serif', serif;
  }
  .cards-container{
    display: flex;
    flex-wrap: wrap;
  }
  .overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.77 );
    z-index: 10;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .modal{
    width: 750px;
    background-color: white;
    padding: 30px;
    border-radius: 10px;
    position: relative;
    display: flex;
    flex-direction: column;
  }
  .modal button{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    cursor: pointer;
    margin-top: 15px;
  }
  .modal .close{
    background-color: red;
    margin-top: 7px;
  }
  .modal p{
    color: red;
  }
  .main-text{
    text-wrap: wrap;
    overflow: hidden;
    word-wrap: break-word;
    font-family: 'IBM Plex Serif', serif;
  }
</style>