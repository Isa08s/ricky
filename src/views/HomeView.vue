<script setup lang="ts">
import { onMounted, ref } from 'vue';

const characters :  any = ref([])

const loadCharacters =  async () =>{
  const response = await fetch('https://rickandmortyapi.com/api/character')
  const data = await response.json()


    characters.value = data.results
    console.log(characters.value)
}

onMounted(() => {
  loadCharacters()
})


</script>

<template>
  <main>
    <div class="flex justify-center items-center mt-8">
      <h1 class="text-3xl font-bold">
        Rick y Morty
      </h1>
    </div>

    <div class="grid grid-cols-6 gap-4 mt-24 mx-10">
      <div v-for="character in characters" :key="character.id" class="rounded-2xl overflow-hidden shadow-2xl">
        <img  :src="character.image" alt="character.name">
        <div class="mt-4 text-center">
          {{ character.name }}
        </div>
      </div>
    </div >
    
  </main>

</template>
