<template>
  <h1 :style="{color: colors[1] }">{{ name.toLowerCase() }}</h1>
  <ul>
    <li  v-for="(color, index) in colorNames" :key="index"
      :style="{color: colors[index % colors.length]}">
      {{color}}
    </li>
  </ul>

  <ul>
    <li  v-for="item in frutaStock" :key="item.name">
      {{item.name}} - {{item.price}}
    </li>
  </ul>
  <button @click.middle="handleKey">Right active</button>

  <button @click="minus">Minus</button>
  <button @click="plus">Plus</button>
  <button @click="reset">Reset</button>
  <button @click="add" :disabled="deactivated">Push</button>

  <div :style="{ color: counter < 0 ? 'red' : 'blue' }">{{ counter }}</div>
  <div>
    <div>
      {{selectedNumbers}}
    </div>
  </div>




</template>

<script setup>

import {computed, reactive, ref} from "vue";
const selectedNumbers = ref([])
const counter = ref(0)
const name = ref('Dynamic')
const colors = ref(['yellow', 'red', 'blue'])
const colorNames = ref(['Yellow', 'Red', 'Blue', "Lala", "lolo"])
const deactivated = ref(false)

function plus(){
  counter.value++
}
function minus(){
  counter.value--
}

function reset(){
  counter.value = 0
}
function handleKey(event) {
  console.log('pressed key', event.target)
}

function add() {
  if (!selectedNumbers.value.includes(counter.value)) {
    selectedNumbers.value.push(counter.value);
  }
}

const arrayFrutas = [
  {
    name: "Manzana",
    price: "$1.00",
    description: "Una manzana",
    stock: 0,
  },
  {
    name: "Pera",
    price: "$2.00",
    description: "Una pera",
    stock: 10,
  },
  {
    name: "Naranja",
    price: "$3.00",
    description: "Una naranja",
    stock: 20,
  },
];

const frutaStock = computed(()=> {
  return arrayFrutas.filter(fruta => fruta.stock > 0)
})


</script>

<style scoped>
.testdiv {
  width: 50%;
  height: 200px;
  border: 1px solid black;
}

</style>