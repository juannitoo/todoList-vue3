<template>
    <div>
    <ul>
      <li v-for="t in thingsToDo" v-bind:key="t.id">
        <div id="delete">
          <button id="delete-btn" @click="deleteThing(t)">X</button>
        </div>
        <div id="thing">
          <div v-if="edition.edit === false 
                    || edition.edit === true && edition.id !== `edit`+t.id">
            {{ t.thing }}
            <span class="edit" @click="editThing(t)">
              Editer
            </span>
          </div>
          <div v-if="edition.edit === true && edition.id === `edit`+t.id">
            <input id="edit-Input" type="text" v-model="t.thing" @keypress.enter="saveThing(t)"/>
            <span class="edit" @click="saveThing(t)">Sauvegarder</span>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';
export default {
  emits : [ "delete-thing", "edit-thing" ],
  props: {
    thingsToDo : {
      type: Array,
      required: true
    }
  },
  setup(props, ctx){
    let edition = ref({edit:false, id: ""})

    const deleteThing = function(thing){
      ctx.emit("delete-thing", thing)
    };
    const editThing = function(thing){
      edition.value = {edit:true, id:"edit"+thing.id,}
    };
    const saveThing = function(thing){
      ctx.emit("edit-thing", thing)
      edition.value = {edit:false, id:""}
    };

    return {
      deleteThing,
      editThing,
      edition,
      saveThing
    };
  },
}
</script>

<style scoped>
ul{
  list-style: none;
  margin: 0;
  padding: 0;
  width : 100%;
}
li{
  width: 100%;
  margin-top: 1rem;
  font-size: 1.5rem;
}
#delete-btn{
  background-color: rgb(255,100,100);
  font-weight: bold;
  color: white;
  border: 1px solid white;
  vertical-align: middle;
}
#delete{
  width: 43%;
  text-align: right;
  margin-right: 1%;
  display: inline-block;
}
#thing{
  display: inline-block; 
  width: 56%;
  text-align: left;
}
.edit{
  color: blue;
  font-size: 1rem;
  font-style: italic;
  margin-left: 0.5rem;
  &:hover{
    text-decoration: underline;
    cursor: pointer;
  }
}
#edit-Input{
  font-size: 1.5rem;
  /* padding: 0.1rem; */
}
#save{
  padding: 0.4rem;
  margin-top : -0.2rem;
}
</style>