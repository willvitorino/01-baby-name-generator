<script setup lang="ts">
import { Gender, Popularity, Length, names } from '@/src/assets/data'

interface OptionState {
  gender: Gender
  popularity: Popularity
  length: Length
}

const options = reactive<OptionState>({
  gender: Gender.GIRL,
  popularity: Popularity.UNIQUE,
  length: Length.SHORT
})

const selectednames = ref<string[]>([])

const optionsList = [
  {
    title: '1) Choose a gender:',
    category: 'gender',
    callback: (value: Gender) => (options.gender = value),
    buttons: [Gender.BOY, Gender.GIRL, Gender.UNISEX]
  },
  {
    title: '2) Choose the name\'s popularity:',
    category: 'popularity',
    callback: (value: Popularity) => (options.popularity = value),
    buttons: [Popularity.TRENDY, Popularity.UNIQUE]
  },
  {
    title: '3) Choose name\'s length:',
    category: 'length',
    callback: (value: Length) => (options.length = value),
    buttons: [Length.LONG, Length.SHORT, Length.ALL]
  }
]

type OptionsKey = keyof typeof options;

function handleSelectedNames() {
  selectednames.value = names
    .filter(name => (name.gender === options.gender))
    .filter(name => (name.popularity === options.popularity))
    .filter(name => ([Length.ALL, name.length].includes(options.length)))
    .map(({ name }) => name)
}

function handleRemoveName(index: number) {
  selectednames.value.splice(index, 1)
}
</script>

<template>
  <div class="app-container">
    <h1>Baby Name Generator</h1>

    <p>Choose your options and click the "Find Names" buttom below.</p>

    <div class="options-container">
      <Option
        v-for="option in optionsList"
        :key="option.title"
        :option="option"
        :value="options[option.category as OptionsKey]"
      />

      <button
        class="primary"
        @click="handleSelectedNames"
      >
        Find Names
      </button>
    </div>

    <div class="cards-container">
      <CardName
        v-for="(name, index) in selectednames"
        :key="`#${index}:${name}`"
        :name="name"
        @remove="() => handleRemoveName(index)"
      />
    </div>
  </div>
</template>

<style scoped>
.app-container {
  width: 100vw;
  max-width: 100vw;
  height: 100vh;
  overflow-x: hidden;
  overflow-y: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  color: rgb(27, 60, 138);
}

.app-container h1 {
  font-size: 2rem;
  margin: 0;
}

.app-container .options-container {
  background-color: rgb(2550 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 90%;
  margin: 2rem auto 0;
  text-align: center;
}

.app-container .options-container .primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}

.app-container .cards-container {
  display: flex;
  width: 90%;
  margin: 2rem 0;
  gap: 2rem;
  flex-wrap: wrap;
  justify-content: space-around;
}
</style>

<style>
@import url('https://fonts.googleapis.com/css2?family=Titillium+Web:ital,wght@0,200;0,300;0,400;0,600;0,700;0,900;1,200;1,300;1,400;1,600;1,700&display=swap');

body {
  font-family: 'Titillium Web', sans-serif;
  padding: 0;
  margin: 0;
}
</style>