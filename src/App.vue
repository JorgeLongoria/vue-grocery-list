<script setup>
import { ref } from 'vue'
import { useStorage } from '@vueuse/core'
import { nanoid } from 'nanoid'
import confetti from 'canvas-confetti'


const newGrocery = ref('')
const groceries = useStorage('groceries', [])

const addGrocery = () => {
  if (newGrocery.value){
    groceries.value.push({ id: nanoid(), name: newGrocery.value  })
    newGrocery.value = ''
  }
}

const deleteGrocery = id => {
  const removeIndex = groceries.value.findIndex(grocery => grocery.id === id)
  groceries.value.splice(removeIndex, 1)
  confetti({ particleCount: 300, spread: 1000, origin: { y: 1 } })
}


</script>

<template>
  <main>
    <h1 class="title">Vue Grocery List 🛒</h1>
    <form class="newGroceryForm" @submit.prevent="addGrocery">
      <input id="newGrocery" autocomplete="off" type="text" placeholder="Add an item to the list" v-model="newGrocery"/>
      <button type="submit">Add</button>
    </form>
    <h3>Pending Items: {{ groceries.length }}</h3>
    <ul>
      <li v-for="grocery in groceries" @click="deleteGrocery(grocery.id)">
        {{ grocery.name }}
      </li>
    </ul>
  </main>
</template>

<style lang="postcss" scoped>
  main{
    @apply mt-9 flex flex-col justify-center items-center;
  
  }
  .title{
    @apply m-2 text-5xl font-light tracking-wider;
  }

  form{
    @apply mt-9 flex focus-within:rounded-lg;
    input{
      @apply bg-white text-black p-2 w-80 text-2xl rounded-l-md;
    }
    button{
      @apply bg-black text-white p-2 text-2xl font-bold rounded-r-md;
      &:hover{
        @apply bg-gray-500;
      }
    }
  }
  ul{
    @apply mt-9 flex flex-col items-center justify-center rounded-lg bg-gray-800;
    li{
      @apply bg-white text-black m-2 p-2 w-96 text-center;
      &:hover{
        @apply bg-gray-500 font-bold cursor-pointer;
      }
    }
  }
</style>
