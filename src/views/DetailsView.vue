<script setup>
import { ref, onMounted } from 'vue';
import { useRoute} from 'vue-router';

const route = useRoute()
const id = route.params.id
const character = ref()

const loadCharacter =  async () =>{
    const response = await fetch(`https://rickandmortyapi.com/api/character/${id}`)
    console.log(response)
    const data = await response.json()
    console.log(data)
    character.value = data
    console.log(character.value)
}
onMounted(() => {
    loadCharacter()
})

    </script>

<template>
<div class="flex justify-center items-center h-screen" v-if="character ">
    <div class="flex flex-col lg:flex-row items-center gap-8 max-w-4xl w-full px-4">
        <!-- Columna de la imagen -->
        <div class="flex justify-center">
            <img 
                :src="character.image" 
                :alt="character.name" 
                class="rounded-full w-48 h-48 border-3 border-blue-500 shadow-lg"
            >
        </div>
        <!-- Columna de la información -->
        <div class="bg-white p-6 rounded-2xl shadow-2xl max-w-md w-full">
            <h1 class="text-3xl font-bold text-center mb-4 text-gray-800">{{ character.name }}</h1>
            <div class="space-y-2 text-gray-600">
                <p class="flex items-center">
                    <span class="font-semibold w-24">Ubicación:</span>
                    <span class="ml-2">{{ character.location.name }}</span>
                </p>
                <p class="flex items-center">
                    <span class="font-semibold w-24">Origen:</span>
                    <span class="ml-2">{{ character.origin.name }}</span>
                </p>
                <p class="flex items-center">
                    <span class="font-semibold w-24">Estado:</span>
                    <span class="ml-2">{{ character.status }}</span>
                </p>
                <p class="flex items-center">
                    <span class="font-semibold w-24">Especie:</span>
                    <span class="ml-2">{{ character.species }}</span>
                </p>
                <p class="flex items-center">
                    <span class="font-semibold w-24">Género:</span>
                    <span class="ml-2">{{ character.gender }}</span>
                </p>
            </div>
        </div>
    </div>
</div>
<!-- 
    <div class="grid grid-cols-1 mt-8 "  v-if="character">
        <div class="flex justify-center">
            <img :src="character.image" :alt="character.name">
        </div>
        <div  class="flex flex-col items-center" mx-auto mt-8 shadow-2xl rounded-2xl w-md>
            <h1 class="text-3xl font-bold mb-3">{{ character.name }}</h1>
            <p><b>Ubicacion: </b>{{ character.location.name }}</p>
            <p><b>Origen: </b>{{ character.origin.name}}</p>
            <p><b>Estado: </b>{{ character.status}}</p>
            <p><b>Especie: </b>{{ character.species }}</p>
            <p><b>Genero: </b>{{ character.gender}}</p>
        </div>
    </div>
-->
</template>

