<template>
  <div class="about">
    <CADPersons />
  </div>
</template>

<script setup>
import CADPersons from '../components/CADPersons.vue'
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
