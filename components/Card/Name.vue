<script setup lang="ts">
interface NameProps {
  name: string
}

defineProps<NameProps>()
const emits = defineEmits(['remove'])

const handleRemove = () => {
  emits('remove')
}
</script>

<template>
  <div class="card">
    <h4>{{ name }}</h4>
    <p @click="handleRemove">&#10006;</p>
  </div>
</template>

<style scoped>
.card {
  background-color: rgb(27, 60, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 0;
  margin: 0;
  position: relative;
}

.card h4 {
  margin: 0.5rem;
  text-align: center;
}

.card p {
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

.card:hover p {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

