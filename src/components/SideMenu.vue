<template>
  <div v-if="isShow" class="overlay" @click.stop="closeMenu"></div>
  <div
    class="sideMenu"
    :style="{ transform: isShow ? 'translateX(0)' : 'translateX(100%)' }"
  >
    <ul class="sideMenu-list">
      <li
        v-for="item in menuData"
        :key="item.key"
        :class="['layer-first', { '-active': levelFirstActive === item.key }]"
        @click.stop="changeTab(1, item.key)"
      >
        <span :class="{ 'text-yellow-300': levelFirstActive === item.key }">{{
          item.text
        }}</span>
        <ul v-if="item.children?.length > 0 && levelFirstActive === item.key">
          <li
            v-for="secondItem in item.children"
            :key="secondItem.key"
            class="layer-second"
            @click.stop="changeTab(2, secondItem.key)"
          >
            <span
              :class="{
                'text-yellow-300': levelSecondActive === secondItem.key,
              }"
              >{{ secondItem.text }}</span
            >
            <ul
              v-if="
                secondItem.children?.length > 0 &&
                levelSecondActive === secondItem.key
              "
            >
              <li
                v-for="thirdItem in secondItem.children"
                :key="thirdItem.key"
                class="layer-third"
                @click.stop="changeTab(3, thirdItem.key)"
              >
                <span
                  :class="{
                    'text-yellow-300': levelThirdActive === thirdItem.key,
                  }"
                  >{{ thirdItem.text }}</span
                >
              </li>
            </ul>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>
<script setup>
import { onMounted, ref, watch } from "vue";
import data from "../json/data.json";
const emit = defineEmits(["menuToggle"]);
const props = defineProps({
  isShow: {
    type: Boolean,
    default: false,
  },
});
const menuData = ref([]);
const levelFirstActive = ref();
const levelSecondActive = ref();
const levelThirdActive = ref();

watch(
  () => props.isShow,
  (val) => {
    if (val) {
      levelFirstActive.value = null;
      levelSecondActive.value = null;
      levelThirdActive.value = null;
    }
  }
);

const changeTab = (level, key) => {
  if (level === 1) {
    levelFirstActive.value = key;
    levelSecondActive.value = null;
    levelThirdActive.value = null;
  } else if (level === 2) {
    levelSecondActive.value = key;
    levelThirdActive.value = null;
  } else {
    levelThirdActive.value = key;
  }
};

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
  &-list {
    @apply text-white;
    li {
      @apply py-1 px-2;
    }
    .layer-first {
      @apply mb-4;
      &.-active {
        @apply bg-gray-400;
      }
    }
    .layer-second {
      @apply indent-[1em];
    }
    .layer-third {
      @apply indent-[2em];
    }
  }
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
