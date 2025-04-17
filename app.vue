<template>
  <main class="flex flex-col gap-8 p-12 min-h-screen items-center bg-gradient-to-b from-red-800 to-black text-white">

    <NuxtLink to="/" class="text-2xl text-white hover:text-red-400">lab 4 and 5 front end</NuxtLink>

    <div class="flex flex-col items-center gap-2">
      <label for="movie">Pick a movie</label>
      <select id="movie" v-model="selectedMovie" class="text-black p-2 rounded border">
        <option>Legally blonde 1</option>
        <option>Legally blonde 2</option>
        <option>Me before you</option>
        <option>The fast and the furious: tokyo drift</option>
      </select>

      <iframe
        v-if="movieEmbeds[selectedMovie]"
        :src="movieEmbeds[selectedMovie]"
        width="560"
        height="315"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
        allowfullscreen
        class="rounded-xl shadow-lg"
      ></iframe>
    </div>

    <div class="flex flex-col items-center gap-4">
      <p>Select a character</p>
      <div class="flex gap-4">
        <label><input type="radio" value="Rori" v-model="selectedPic" class="mx-2">Rori</label>
        <label><input type="radio" value="Lorelai" v-model="selectedPic" class="mx-2">Lorelai</label>
        <label><input type="radio" value="Fiona" v-model="selectedPic" class="mx-2">Fiona</label>
      </div>

      <div v-if="characterImages[selectedPic]" class="blockcap">
        <img :src="characterImages[selectedPic].image" class="w-60 h-68 pt-2" />
        <p class="text-xl">{{ characterImages[selectedPic].name }}</p>
      </div>
    </div>

    <div class="flex gap-4 flex-wrap">
      <div v-for="(pic, index) in genpic" :key="index" class="blockfor">
        <img :src="pic.image" class="w-60 h-60 pt-2" />
        <p class="text-xl">{{ pic.name }}</p>
      </div>
    </div>
      
    <div class="flex flex-col items-center gap-4 w-full max-w-md mt-10">
      <h2 class="text-2xl font-bold">Mini Calculator</h2>
      <input type="number" v-model.number="frst" placeholder="First number" class="text-black p-2 rounded w-full" />
      <input type="number" v-model.number="scnd" placeholder="Second number" class="text-black p-2 rounded w-full" />

      <div class="flex gap-4">
        <button @click="setSign('+')" class="bg-red-600 px-4 py-2 rounded hover:bg-red-400">+</button>
        <button @click="setSign('-')" class="bg-red-600 px-4 py-2 rounded hover:bg-red-400">-</button>
        <button @click="setSign('*')" class="bg-red-600 px-4 py-2 rounded hover:bg-red-400">*</button>
        <button @click="setSign('/')" class="bg-red-600 px-4 py-2 rounded hover:bg-red-400">/</button>
      </div>

      <p class="text-xl font-semibold mt-2">Result: {{ calc }}</p>
    </div>

  </main>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const selectedMovie = ref('Legally blonde 1')
const selectedPic = ref('')

const movieEmbeds = {
  'Legally blonde 1': 'https://www.youtube.com/embed/vWOHwI_FgAo?si=z-7Vh9E5w20VnHrq',
  'Legally blonde 2': 'https://www.youtube.com/embed/I25jkF0bdJk?si=oufrF9yJb0_Yw2tR',
  'Me before you': 'https://www.youtube.com/embed/T0MmkG_nG1U?si=9A5PSU4_F6Tw7PAH',
  'The fast and the furious: tokyo drift': 'https://www.youtube.com/embed/p8HQ2JLlc4E?si=Da0dQA9ABTcJc1u4'
}

const characterImages = {
  Rori: { name: 'Rori', image: '/img/rori.png' },
  Lorelai: { name: 'Lorelai', image: '/img/lorelai.png' },
  Fiona: { name: 'Fiona', image: '/img/fiona.png' }
}

const genpic = [
  { name: 'Kev', image: '/img/kev.png' },
  { name: 'Blair', image: '/img/blair.png' },
  { name: 'Lip', image: '/img/lip.png' }
]

// Calculator logic
const frst = ref(0)
const scnd = ref(0)
const signn = ref('+')

const setSign = (op: string): void => {
  signn.value = op
}

const calc = computed((): number => {
  switch (signn.value) {
    case '+':
      return frst.value + scnd.value
    case '-':
      return frst.value - scnd.value
    case '*':
      return frst.value * scnd.value
    case '/':
      try {
        return parseFloat((frst.value / scnd.value).toFixed(1))
      } catch (error) {
        console.log("Division error")
        return 0
      }
    default:
      return 0
  }
})
</script>

<style scoped>
.blockcap {
  @apply flex flex-col gap-2 border border-red-500 bg-black w-72 h-auto items-center rounded-xl shadow-md hover:bg-red-900 text-white;
}

.blockfor {
  @apply flex flex-col gap-2 border border-red-500 bg-black w-72 h-auto items-center rounded-xl shadow-md hover:bg-red-900 text-white;
}
</style>
