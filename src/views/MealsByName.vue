<template>
  <div class="p-8">
    <v-text-field
      label="Search for meals"
      class="w-full"
      v-model="keyword"
      @change="searchMeals"
      hide-details="auto"
    ></v-text-field>
  </div>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, ref } from "vue";
import { useRoute } from "vue-router";
import { onMounted } from "vue";
import store from "../store";
import MealItem from "../components/MealItem.vue";
import Meals from "../components/Meals.vue";

const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  if (keyword.value) {
    store.dispatch("searchMeals", keyword.value);
  } else {
    store.commit("setSearchedMeals", []);
  }
}

onMounted(() => {
  keyword.value = route.params.name;
  if (keyword.value) {
    searchMeals();
  }
});
</script>
