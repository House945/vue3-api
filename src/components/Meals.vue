<template>
  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-4">
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>
  <div
    v-if="!meals?.length"
    class="flex-col items-center text-center justify-center text-gray-600"
  >
    <p>
      There are no available matches meeting your criteria. Please try again.
    </p>
    <v-img cover class="w-full" src="src/assets/burgir.png" />
  </div>
</template>

<script setup>
import MealItem from "./MealItem.vue";

const { meals } = defineProps({
  meals: {
    required: true,
    type: Array,
  },
});
</script>
