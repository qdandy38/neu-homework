<template>
  <header class="w-full h-[60px] bg-white flex justify-end p-2">
    <button class="btn">
      <span class="line"></span>
      <span class="line"></span>
      <span class="line"></span>
    </button>
  </header>
</template>
<script setup></script>
<style lang="scss" scoped>
.btn {
  @apply border
  border-black
  rounded-lg
  p-3
  flex
  flex-col
  gap-2
  bg-gray-200;
}
.line {
  @apply block
  w-[30px]
  h-[1px]
  bg-black
  mx-auto;
}
</style>
