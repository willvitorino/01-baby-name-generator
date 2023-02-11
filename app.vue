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

function handleSelectedNames() {
  selectednames.value = names
    .filter(name => (name.gender === options.gender))
    .filter(name => (name.popularity === options.popularity))
    .filter(name => ([Length.ALL, name.length].includes(options.length)))
    .map(({ name }) => name)
}

</script>

<template>
  <div class="app-container">
    <h1>Baby Name Generator</h1>

    <p>Choose your options and click the "Find Names" buttom below.</p>

    <div class="options-container">
      <div class="option-container">
        <h4>1) Coose a gender:</h4>

        <div class="option-buttons">
          <button
            :class="{'option-active': options.gender === Gender.BOY}"
            class="option"
            @click="options.gender = Gender.BOY"
          >
            Boy
          </button>

          <button
            :class="{'option-active': options.gender === Gender.UNISEX}"
            class="option"
            @click="options.gender = Gender.UNISEX"
          >
            Unisex
          </button>

          <button
            :class="{'option-active': options.gender === Gender.GIRL}"
            class="option"
            @click="options.gender = Gender.GIRL"
          >
            Girl
          </button>
        </div>
      </div>

      <div class="option-container">
        <h4>2) Choose the name's popularity:</h4>

        <div class="option-buttons">
          <button
            :class="{'option-active': options.popularity === Popularity.TRENDY}"
            class="option"
            @click="options.popularity = Popularity.TRENDY"
          >
            Trendy
          </button>

          <button
            :class="{'option-active': options.popularity === Popularity.UNIQUE}"
            class="option"
            @click="options.popularity = Popularity.UNIQUE"
          >
            Unique
          </button>
        </div>
      </div>

      <div class="option-container">
        <h4>3) Choose name's length:</h4>

        <div class="option-buttons">
          <button
            :class="{'option-active': options.length === Length.LONG}"
            class="option"
            @click="options.length = Length.LONG"
          >
            Long
          </button>

          <button
            :class="{'option-active': options.length === Length.ALL}"
            class="option"
            @click="options.length = Length.ALL"
          >
            All
          </button>

          <button
            :class="{'option-active': options.length === Length.SHORT}"
            class="option"
            @click="options.length = Length.SHORT"
          >
            Short
          </button>
        </div>
      </div>

      <button
        class="primary"
        @click="handleSelectedNames"
      >
        Find Names
      </button>
    </div>

    <div class="cards-container">
      <div
        v-for="(name, index) in selectednames"
        :key="`#${index}:${name}`"
        class="card"
      >
        <h4>{{ name }}</h4>
        <p>&#10006;</p>
      </div>
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

.app-container .options-container .option-container {
  margin-bottom: 2rem;
}

.app-container .options-container .option-container .option-buttons .option {
  background-color: #fff;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}

.app-container .options-container .option-container .option-buttons .option:first-child {
  border-radius: 1rem 0 0 1rem;
}

.app-container .options-container .option-container .option-buttons .option:last-child {
  border-radius: 0 1rem 1rem 0;
}

.app-container .options-container .option-container .option-buttons .option.option-active {
  background-color: rgb(249, 87, 89);
  color: white;
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

.app-container .cards-container .card {
  background-color: rgb(27, 60, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 0;
  margin: 0;
  position: relative;
}

.app-container .cards-container .card h4 {
  margin: 0.5rem;
  text-align: center;
}

.app-container .cards-container .card p {
  position: absolute;
  right: 0;
  top: 0;
  bottom: 0;
  cursor: pointer;
  color: red;
  margin: 0;
  width: 1.5rem;
  display: none;
}

.app-container .cards-container .card:hover p {
  display: flex;
  justify-content: center;
  align-items: center;
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