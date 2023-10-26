<template>

  <h1>Todo list</h1>
  <img alt="Vue logo" src="./assets/logo.png">

  <TodoForm @add="saveThings" />

  <h3>{{ thingsToDo.length }} chose{{ thingsToDo.length > 1 ? "s" : ""  }} à faire</h3>
  
  <TodoList 
    :thingsToDo="thingsToDo" 
    @delete-thing="deleteThing"
    @edit-thing="editThing"
  />

</template>

<script>
import { ref } from 'vue';
import TodoForm from './components/Todo-form.vue';
import TodoList from './components/Todo-list.vue';
export default {
  name: 'App',
  components: {
    TodoForm, 
    TodoList
  },
  setup(){
    let thingsToDo = ref([]);
    const saveThings = function(data){
      thingsToDo.value.push({thing: data, id: Date.now()})
    };
    const deleteThing = function(thing){
      thingsToDo.value = thingsToDo.value.filter(t => t.id !== thing.id )
    };
    const editThing = function(thing){
      let thingIndex = thingsToDo.value.indexOf(thing)
      thingsToDo.value.splice(thingIndex, 1, thing)
    };
    return{
      saveThings, thingsToDo, deleteThing, editThing
    };
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
