<script setup>

</script>

<template>
  <main>
    <h1 class="title">Vue Grocery List 🛒</h1>
    <form class="newGroceryForm">
      <input id="newGrocery" autocomplete="off" type="text" placeholder="Add an item to the list" />
      <button id="addButton" type="submit">Add</button>
    </form>
  </main>
</template>

<style lang="postcss" scoped>
  main{
    @apply flex flex-col justify-center items-center;
  
  }
  .title{
    @apply m-2 text-5xl font-light tracking-wider;
  }

  form{
    @apply mt-8 flex focus-within:ring-8 focus-within:rounded-lg;
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
</style>
