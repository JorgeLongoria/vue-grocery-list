<script setup>
import { ref } from 'vue'
import { nanoid } from 'nanoid'

const newGrocery = ref('')
const gorceries = ref([])

const addGrocery = () => {
  if (newGrocery.value){
    gorceries.value.push({id: nanoid(), name: newGrocery.value})
    newGrocery.value = ''
  }
}

const deleteGrocery = () => {
  newGrocery.value = 'deleting new item'
}


</script>

<template>
  <main>
    <h1 class="title">Vue Grocery List 🛒</h1>
    <form class="newGroceryForm" @submit.prevent="addGrocery">
      <input id="newGrocery" autocomplete="off" type="text" placeholder="Add an item to the list" v-model="newGrocery"/>
      <button type="submit">Add</button>
    </form>
    <ul>
      <li @click="deleteGrocery">{{ newGrocery }}</li>
    </ul>
  </main>
  <pre>{{gorceries}}</pre>
</template>

<style lang="postcss" scoped>
  main{
    @apply flex flex-col justify-center items-center;
  
  }
  .title{
    @apply m-2 text-5xl font-light tracking-wider;
  }

  form{
    @apply flex focus-within:ring-8 focus-within:rounded-lg;
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
    @apply flex flex-col items-center justify-center rounded-md;
    li{
      @apply bg-white text-black m-2 p-2 w-96 text-center;
      &:hover{
        @apply bg-gray-500 font-bold cursor-pointer;
      }
    }
  }
</style>
