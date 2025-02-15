<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { useRouter } from 'vue-router';


const characters :  any = ref([])
const page:any = ref(1)
const router = useRouter()

const incrementarPage = () => {
  page.value++
  loadCharacters()
}
const descrementPage = () => {
  if (page.value > 1){
    page.value--
    loadCharacters()
  }
}

const loadCharacters =  async () =>{
  const response = await fetch(`https://rickandmortyapi.com/api/character?page=${page.value}`)
  const data = await response.json()
  characters.value = data.results

    console.log(characters.value)
}
const seeCharacterDetails = (character_id: number) => {
  router.push(`/details/${character_id}`)
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

    <div class="flex items-center justify-center space-x-4">
  <button class="border-2 border-gray-300 rounded-full p-2 bg-blue-500 text-white hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50 shadow-md" @click="descrementPage">
    -
  </button>
  <div class="text-xl font-semibold">
    {{ page }}
  </div>
  <button class="border-2 border-gray-300 rounded-full p-2 bg-blue-500 text-white hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50 shadow-md" @click="incrementarPage">
    +
  </button>
    </div>

    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-7 mt-24 mx-10">
      <div v-for="character in characters" :key="character.id"  class="rounded-2xl overflow-hidden shadow-2xl">
        <div @click="seeCharacterDetails(character.id)">
          <img  :src="character.image" alt="character.name">
          <div class="mt-4 text-center">
            {{ character.name }}
          </div>
        </div>
      </div>
    </div >
    
  </main>

</template>
