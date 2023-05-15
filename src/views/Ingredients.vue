<template>
  <v-container class="p-8 pb-0 text-orange-500">
    <h1 class="text-4xl font-semibold mb-4">Ingredients</h1>
    <v-text-field
      class="text-black"
      label="Search for ingredients"
      v-model="keyword"
      outlined
      hide-details="auto"
    ></v-text-field>

    <v-row class="mt-4">
      <v-col
        cols="12"
        sm="6"
        md="6"
        lg="4"
        v-for="ingredient in searchedIngredients"
        :key="ingredient.idIngredient"
      >
        <v-card class="ingredient-card" @click="openIngredient(ingredient)">
          <v-card-text>
            <h3 class="text-2xl font-bold mb-2">
              {{ ingredient.strIngredient }}
            </h3>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col v-if="searchedIngredients.length === 0" cols="12">
        <div class="flex justify-center text-gray-600 p-8">
          There are currently no ingredients in the database with this search
          term.
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { onMounted, ref, computed } from "vue";
import { useRouter } from "vue-router";

import axiosClient from "../axiosClient";
import store from "../store";

const router = useRouter();
const keyword = ref("");
const ingredients = ref([]);
const searchedIngredients = computed(() => {
  if (!keyword.value) return ingredients.value;
  return ingredients.value.filter((ingredient) =>
    (ingredient.strIngredient || "")
      .toLowerCase()
      .includes(keyword.value.toLowerCase())
  );
});

function openIngredient(ingredient) {
  store.commit("setIngredient", ingredient);
  router.push({
    name: "byIngredient",
    params: { ingredient: ingredient.strIngredient },
  });
}

onMounted(() => {
  axiosClient.get("list.php?i=list").then(({ data }) => {
    ingredients.value = data.meals;
  });
});
</script>

<style scoped>
.ingredient-card {
  cursor: pointer;
  transition: transform 0.3s ease;
}

.ingredient-card:hover {
  transform: scale(1.05);
  color: orange;
}
</style>
