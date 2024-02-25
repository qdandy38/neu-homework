<template>
  <div v-if="isShow" class="overlay" @click.stop="closeMenu"></div>
  <div
    class="sideMenu"
    :style="{ transform: isShow ? 'translateX(0)' : 'translateX(100%)' }"
  >
    <MenuLevel
      :list="menuData"
      :level="1"
      :activeMap="activeMap"
      @changeActive="changeActive"
    />
  </div>
</template>
<script setup>
import { onMounted, ref, watch } from "vue";
import data from "../json/data.json";
import MenuLevel from "./MenuLevel.vue";
const emit = defineEmits(["menuToggle"]);
const props = defineProps({
  isShow: {
    type: Boolean,
    default: false,
  },
});
const menuData = ref([]);
const activeMap = ref({});
const changeActive = (level, key) => {
  activeMap.value[level] = key;
  Object.keys(activeMap.value).forEach((n) => {
    if (n > level) {
      activeMap.value[n] = "";
    }
  });
};

watch(
  () => props.isShow,
  (val) => {
    if (val) {
      activeMap.value = {};
    }
  }
);

const closeMenu = () => {
  emit("menuToggle");
};

onMounted(() => {
  menuData.value = data;
});
</script>
<style lang="scss" scoped>
.sideMenu {
  transition: transform 0.3s ease;
  @apply py-4
  px-2
  fixed
  top-0
  right-0
  w-[200px]
  h-screen
  bg-black
  z-[99];
}
.overlay {
  @apply fixed
  top-0
  left-0
  w-full
  h-full
  bg-transparent
  z-[98];
}
</style>
