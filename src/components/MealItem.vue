<template>
  <v-card class="bigger">
    <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
      <v-img
        class="rounded-t-2xl"
        :src="meal.strMealThumb"
        :alt="meal.strMeal"
      ></v-img>
      <v-card-title class="p-3 font-semibold">{{ meal.strMeal }}</v-card-title>
      <v-card-text class="px-3">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt, commodi
        aliquam quis ratione possimus eius minima iusto iste, inventore
        exercitationem aliquid sed ipsum laborum quasi aspernatur repellendus
        soluta, minus tempore.
      </v-card-text>
    </router-link>
    <v-card-actions class="p-3">
      <v-btn
        :href="meal.strYoutube"
        target="_blank"
        class="hover:bg-orange-500 hover:text-white"
        outlined
        >Youtube</v-btn
      >
      <v-btn
        :href="meal.strSource"
        target="_blank"
        class="hover:bg-orange-500 hover:text-white"
        outlined
        >Info</v-btn
      >
    </v-card-actions>
  </v-card>
</template>
<script setup>
const props = defineProps({
  meal: {
    required: true,
    type: Object,
  },
});
</script>
<style scoped>
.bigger:hover {
  transform: scale(1.05); /* Increase the scale value as desired */
  transition: transform 0.3s ease-in-out; /* Add a smooth transition effect */
}
</style>
