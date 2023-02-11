<script setup lang="ts">
import { Gender, Length, Popularity } from '@/src/assets/data';

interface OptionProps {
  option: {
    title: string
    category: string
    callback: Function
    buttons: Gender[] | Popularity[] | Length[]
  },
  value: Gender | Popularity | Length
}

const props = defineProps<OptionProps>()
</script>

<template>
  <div class="option-container">
    <h4>{{ option.title }}</h4>

    <div class="option-buttons">
      <button
        v-for="btn in option.buttons"
        :key="btn"
        :class="{ 'option-active': value === btn }"
        @click="option.callback(btn)"
        class="option"
      >
        {{ btn }}
      </button>
      <!-- <button
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
      </button> -->
    </div>
  </div>
</template>

<style scoped>
.option-container {
  margin-bottom: 2rem;
}

.option-container .option-buttons .option {
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

.option-container .option-buttons .option:first-child {
  border-radius: 1rem 0 0 1rem;
}

.option-container .option-buttons .option:last-child {
  border-radius: 0 1rem 1rem 0;
}

.option-container .option-buttons .option.option-active {
  background-color: rgb(249, 87, 89);
  color: white;
}
</style>
