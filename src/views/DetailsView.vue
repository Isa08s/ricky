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
    <div v-if="character">
        {{ character.name }}
    </div>

</template>

