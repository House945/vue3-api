<template>
  <header
    class="bg-white shadow h-16 flex justify-between items-stretch rounded-2xl"
  >
    <router-link
      :to="{ name: 'home' }"
      class="inline-flex items-center h-full px-5 text-orange-500 font-semibold"
    >
      Home
    </router-link>

    <!-- Mobile Mode -->
    <div class="md:hidden">
      <button
        @click="toggleMenu"
        :class="{ 'text-orange-500': !showMenu, 'text-white': showMenu }"
        class="inline-flex items-center px-3 py-2 border rounded border-orange-500 hover:text-white hover:bg-orange-500 focus:outline-none"
      >
        <span class="mdi" :class="[showMenu ? 'mdi-close' : 'mdi-menu']"></span>
      </button>
    </div>

    <!-- Desktop Mode -->
    <div class="hidden md:flex items-center gap-2">
      <router-link
        :to="{ name: 'byName' }"
        class="inline-flex items-center px-2 h-full transition-colors hover:bg-orange-500 hover:text-white"
      >
        Search Meals
      </router-link>
      <router-link
        :to="{ name: 'byLetter' }"
        class="inline-flex items-center px-2 h-full transition-colors hover:bg-orange-500 hover:text-white"
      >
        Meals By Letter
      </router-link>
      <router-link
        :to="{ name: 'ingredients' }"
        class="inline-flex items-center px-3 h-full transition-colors hover:bg-orange-500 hover:text-white"
      >
        Meals By Ingredients
      </router-link>
    </div>

    <!-- Mobile Menu -->
    <div
      v-if="showMenu"
      class="md:hidden absolute top-0 right-0 left-0 bg-white z-10"
    >
      <div class="flex flex-col gap-1 py-2 px-4">
        <button
          @click="toggleMenu"
          class="text-orange-500 inline-flex items-center px-3 py-2 border rounded border-orange-500 hover:text-white hover:bg-orange-500 focus:outline-none"
        >
          <span
            class="mdi"
            :class="[showMenu ? 'mdi-close' : 'mdi-menu']"
          ></span>
        </button>
        <router-link
          :to="{ name: 'byName' }"
          class="block px-2 py-1 transition-colors hover:bg-orange-500 hover:text-white"
          @click="toggleMenu"
        >
          Search Meals
        </router-link>
        <router-link
          :to="{ name: 'byLetter' }"
          class="block px-2 py-1 transition-colors hover:bg-orange-500 hover:text-white"
          @click="toggleMenu"
        >
          Meals By Letter
        </router-link>
        <router-link
          :to="{ name: 'ingredients' }"
          class="block px-2 py-1 transition-colors hover:bg-orange-500 hover:text-white"
          @click="toggleMenu"
        >
          Meals By Ingredients
        </router-link>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref } from "vue";

const showMenu = ref(false);

const toggleMenu = () => {
  showMenu.value = !showMenu.value;
};
</script>

<style scoped>
.mdi {
  font-size: 1.5rem;
}
</style>
