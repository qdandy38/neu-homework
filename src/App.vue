<template>
  <div class="w-full h-screen bg-gray-300 overflow-hidden">
    <Header @menuToggle="menuToggle" />
    <Main />
    <SideMenu :isShow="showMenu" @menuToggle="menuToggle" />
  </div>
</template>
<script setup>
import { ref } from "vue";
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import SideMenu from "./components/SideMenu.vue";
const showMenu = ref(false);
const menuToggle = () => {
  showMenu.value = !showMenu.value;
};
</script>
<style scoped></style>
