<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
import HomeView from "./views/HomeView.vue";
</script>

<template>
  <div class="p-14">
    <RouterLink class="flex justify-center text-4xl text-yellow-700" to="/">
    </RouterLink>
  </div>
  <RouterView/>
</template>

<style>
</style>
