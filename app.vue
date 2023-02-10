<script setup lang="ts">

enum Gender {
  GIRL = 'gril',
  BOY = 'boy',
  UNISEX = 'unisex'
}

enum Popularity {
  UNIQUE = 'unique',
  TRENDY = 'trendy'
}

enum Length {
  LONG = 'long',
  ALL = 'all',
  SHORT = 'short',
}

interface OptionState {
  gender: Gender
  popularity: Popularity
  length: string
}

const options = reactive<OptionState>({
  gender: Gender.GIRL,
  popularity: Popularity.UNIQUE,
  length: Length.SHORT
})
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
          >
            Boy
          </button>

          <button
            :class="{'option-active': options.gender === Gender.UNISEX}"
            class="option"
          >
            Unisex
          </button>

          <button
            :class="{'option-active': options.gender === Gender.GIRL}"
            class="option"
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
          >
            Trendy
          </button>

          <button
            :class="{'option-active': options.popularity === Popularity.UNIQUE}"
            class="option"
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
          >
            Long
          </button>

          <button
            :class="{'option-active': options.length === Length.ALL}"
            class="option"
          >
            All
          </button>

          <button
            :class="{'option-active': options.length === Length.SHORT}"
            class="option"
          >
            Short
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-container {
  width: 100vw;
  height: 100vh;
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
  width: 95%;
  margin: 4rem auto 0;
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
</style>

<style>
@import url('https://fonts.googleapis.com/css2?family=Titillium+Web:ital,wght@0,200;0,300;0,400;0,600;0,700;0,900;1,200;1,300;1,400;1,600;1,700&display=swap');

body {
  font-family: 'Titillium Web', sans-serif;
  padding: 0;
  margin: 0;
}
</style>