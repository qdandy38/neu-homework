<template>
  <ul class="menuLevel">
    <li
      v-for="item in list"
      :key="item.key"
      :class="[
        `ident-[${level - 1}rem]`,
        { '-active': activeMap[level] === item.key },
      ]"
      @click.stop="changeTab(level, item.key)"
    >
      <span :class="{ 'text-yellow-300': activeMap[level] === item.key }">{{
        item.text
      }}</span>
      <MenuLevel
        v-if="item.children?.length > 0 && activeMap[level] === item.key"
        :list="item.children"
        :level="level + 1"
        :activeMap="activeMap"
        @changeActive="changeTab"
      />
    </li>
  </ul>
</template>
<script setup>
import { computed } from "vue";
import MenuLevel from "./MenuLevel.vue";

const emit = defineEmits(["changeActive"]);
const props = defineProps({
  list: {
    type: Array,
    default: [],
  },
  level: {
    type: Number,
    default: 1,
  },
  activeMap: {
    type: Object,
    default: {},
  },
});

const changeTab = (level, key) => {
  emit("changeActive", level, key);
};
</script>
<style lang="scss" scoped>
.menuLevel {
  @apply text-white;
  li {
    @apply py-1 px-2;
    &.-active {
      @apply bg-gray-400;
    }
  }
}
</style>
