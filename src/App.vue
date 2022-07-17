<script>
import CalculatorComponent from './components/CalculatorComponent.vue';

export default {
  components: {
    CalculatorComponent,
  },
};
</script>

<template>
  <main class="h-screen pt-24 bg-zinc-900">
    <CalculatorComponent />
  </main>
</template>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
