<template>
  <form @submit.prevent="addThings">
    <label for="things">Choses à faire :</label>
    <input type="text" name="things" v-model="thingsToDo" placeholder="Saisissez ici"/>
    <br>
    <button type="submit">Ajouter</button>
  </form>
</template>

<script>
import { ref } from 'vue';

export default {
  setup(props, context){
    let thingsToDo = ref("");
    const addThings = function (){
      context.emit("add", thingsToDo.value)
      thingsToDo.value = ""
    };

    return {
      thingsToDo,
      addThings,
    };
  }
}
</script>

<style scoped>
  label, input {
    display: block;
    font-size: 1.8rem;
  }
  input, button{
    margin: 0 auto;
    text-align: center;
  }
  button, input{
    padding : 0.7rem;
    font-size: 1.5rem;
  } 
</style>