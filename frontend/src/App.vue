<template>
  <div>
    <h1>Compteur {{ counter }}</h1>
    <div v-show="counter > 5">Vous avez cliqué plus de 5 fois</div>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>



    <div v-for="participant in participants" :key="participant.id" style="margin:5px; padding:5px; display:flex; justify-content: center;">

      <div>
        id : {{ participant.id }}
      </div>

      <div>
        <select v-model="participant.type" @change="selectType(participant.id)">
          <option v-for="type in types" :key="type">{{ type }}</option>
        </select>
      </div>

      <div v-if="participant.type == types[0]" @change="selectTypeAB(participant.id)">
        <select v-model="participant.typeA">
          <option v-for="typeA in typesA" :key="typeA">{{ typeA }}</option>
        </select>
      </div>

      <div v-if="participant.typeA == typesA[0]">
        <select v-model="participant.typeA1">
          <option v-for="typeA1 in typesA1" :key="typeA1">{{ typeA1 }}</option>
        </select>
      </div>

      <div v-if="participant.typeA == typesA[1]">
        <select v-model="participant.typeA2">
          <option v-for="typeA2 in typesA2" :key="typeA2">{{ typeA2 }}</option>
        </select>
      </div>

      <div v-if="participant.type == types[1]" @change="selectTypeAB(participant.id)">
        <select v-model="participant.typeB">
          <option v-for="typeB in typesB" :key="typeB">{{ typeB }}</option>
        </select>
      </div>

      <div v-if="participant.typeB == typesB[0]">
        <select v-model="participant.typeB1">
          <option v-for="typeB1 in typesB1" :key="typeB1">{{ typeB1 }}</option>
        </select>
      </div>

      <div v-if="participant.typeB == typesB[1]">
        <select v-model="participant.typeB2">
          <option v-for="typeB2 in typesB2" :key="typeB2">{{ typeB2 }}</option>
        </select>
      </div>
      
      <div style="margin:5px;">Type : {{ participant.type }}</div>
      <div v-if="participant.typeA != null" style="margin:5px;">TypeA : {{ participant.typeA }}</div>
      <div v-if="participant.typeA1 != null" style="margin:5px;">TypeA1 : {{ participant.typeA1 }}</div>
      <div v-if="participant.typeA2 != null" style="margin:5px;">TypeA2 : {{ participant.typeA2 }}</div>
      <div v-if="participant.typeB != null" style="margin:5px;">TypeB : {{ participant.typeB }}</div>
      <div v-if="participant.typeB1 != null" style="margin:5px;">TypeB1 : {{ participant.typeB1 }}</div>
      <div v-if="participant.typeB2 != null" style="margin:5px;">TypeB2 : {{ participant.typeB2 }}</div>
    
      <button @click="remove(participant.id)">Remove</button>
      
    </div>
    
    <button @click="add">Add</button>

  </div>
</template>

<script setup>
import {ref} from 'vue'

const types = [ "A", "B" ]
const typesA = [ "A1", "A2" ]
const typesA1 = [ "A1a", "A1b", "A1c" ]
const typesA2 = [ "A2a", "A2b", "A2c" ]
const typesB = [ "B1", "B2" ]
const typesB1 = [ "B1a", "B1b", "B1c" ]
const typesB2 = [ "B2a", "B2b", "B2c" ]

// const participants = ref({
//   id : 0,
//   A : {

//   }
// })

const participants = ref([
  { 
    id : 0, 
    type : types[0], 
    typeA : typesA[0],
    typeA1 : typesA1[0],
    typeA2 : null,
    typeB : null,
    typeB1 : null,
    typeB2 : null,
  },
  { 
    id : 1, 
    type : types[1], 
    typeA : null,
    typeA1 : null,
    typeA2 : null,
    typeB : typesB[1],
    typeB1 : null,
    typeB2 : typesB2[0],
  },
])


const counter = ref(0)
counter.value = 3
const increment = () => {
  counter.value++;
}

const decrement = () => {
  counter.value--;
}

const selectType = (id) => {
  let participant = participants.value.filter(p => p.id === id)[0]
  participant.typeA = null
  participant.typeA1 = null
  participant.typeA2 = null
  participant.typeB = null
  participant.typeB1 = null
  participant.typeB2 = null
}

const selectTypeAB = (id) => {
  const participant = participants.value.filter(p => p.id === id)[0]
  participant.typeA1 = null
  participant.typeA2 = null
  participant.typeB1 = null
  participant.typeB2 = null
}

const add = () => {
  const index = participants.value.length === 0 ? 0 : Math.max(...participants.value.map(p => p.id)) + 1;
  participants.value.push({ 
    id : index, 
    type : types[1], 
    typeA : null,
    typeA1 : null,
    typeA2 : null,
    typeB : null,
    typeB1 : null,
    typeB2 : null,
  })
}

const remove = (id) => {
  participants.value = participants.value.filter(p => p.id !== id);
}

</script>

<style>
h1 {
  color : red;
}
</style>