<template>
  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-4">
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>
  <div
    v-if="!meals?.length"
    class="flex-col items-center text-center justify-center text-gray-600"
  >
    <v-img cover class="w-full" :src="getImageSrc('burgir.png')" alt="burgir" />
  </div>
</template>

<script setup>
import MealItem from "./MealItem.vue";
const getImageSrc = (fileName) => {
  return `${import.meta.env.BASE_URL}${fileName}`;
};

const { meals } = defineProps({
  meals: {
    required: true,
    type: Array,
  },
});
</script>
