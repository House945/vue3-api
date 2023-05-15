<template>
  <v-container class="max-w-[800px] mx-auto">
    <h1 class="text-5xl font-semibold mb-5">{{ meal.strMeal }}</h1>
    <v-card>
      <v-img
        :src="meal.strMealThumb"
        max-height="350"
        cover
        class="w-full rounded-lg shadow-xl h-[350px] object-none"
      ></v-img>
      <v-card-title class="text-h6">
        <v-row class="text-lg py-2">
          <v-col cols="12" sm="4">
            <strong class="font-semibold">Category:</strong>
            {{ meal.strCategory }}
          </v-col>
          <v-col cols="12" sm="4">
            <strong class="font-semibold">Area: </strong>{{ meal.strArea }}
          </v-col>
          <v-col cols="12" sm="4">
            <strong class="font-semibold">Tags: </strong>
            <span v-if="meal.strTags">
              {{ meal.strTags.split(",").slice(0, 2).join(", ") }}
            </span>
            <span v-else>no tags</span>
          </v-col>
        </v-row>
      </v-card-title>
    </v-card>

    <div class="mx-3 mt-5">
      {{ meal.strInstructions }}
    </div>
    <v-row class="mt-5">
      <v-col cols="12" sm="6">
        <h2 class="text-2xl font-semibold mb-2">Ingredients</h2>
        <ul>
          <template v-for="(el, index) of new Array(20)">
            <li v-if="meal[`strIngredient${index + 1}`]">
              <p>{{ index + 1 }}. {{ meal[`strIngredient${index + 1}`] }}</p>
            </li>
          </template>
        </ul>
      </v-col>
      <v-col cols="12" sm="6">
        <h2 class="text-2xl font-semibold mb-2">Measures</h2>
        <ul>
          <template v-for="(el, index) of new Array(20)">
            <li v-if="meal[`strMeasure${index + 1}`]">
              <p>{{ index + 1 }}. {{ meal[`strMeasure${index + 1}`] }}</p>
            </li>
          </template>
        </ul>
      </v-col>
    </v-row>
    <v-row class="p-3 mt-5">
      <v-btn :href="meal.strYoutube" target="_blank" color="primary"
        >Watch on Youtube</v-btn
      >
      <v-btn :href="meal.strSource" target="_blank" color="primary"
        >More Info</v-btn
      >
      <router-link to="/by-name" class="v-btn" color="primary"
        >Back to Meals</router-link
      >
    </v-row>
  </v-container>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";

const route = useRoute();
const meal = ref({});

onMounted(() => {
  axiosClient.get(`/lookup.php?i=${route.params.id}`).then(({ data }) => {
    meal.value = data.meals[0] || "Drink with requested id not found";
  });
});
</script>
