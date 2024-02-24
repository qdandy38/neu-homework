<template>
  <section class="main">
    <div class="container">
      <div v-for="i in 9" :key="i" class="col">
        <div class="col-bg"></div>
        <div v-if="[1, 3, 7, 9].includes(i)" class="ball -ballMoving"></div>
      </div>
    </div>
  </section>
</template>
<script setup></script>
<style lang="scss" scoped>
@keyframes blink {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.6;
  }
  100% {
    opacity: 1;
  }
}
@keyframes ballMove {
  0% {
    transform: translateX(-50%) translateY(-50%);
  }
  100% {
    transform: translateX(calc(-50% + 30vh)) translateY(-50%);
  }
}

.-blinking {
  animation: blink 1s ease-in-out infinite;
}
.-ballMoving {
  animation: ballMove 1s ease-in-out infinite;
}
.main {
  height: calc(100% - 60px);
  @apply w-full
  flex
  justify-center
  items-center;
}
.container {
  @apply w-full
  grid
  grid-cols-3
  gap-1
  px-1;
}
.col {
  @apply relative;
  &-bg {
    background: radial-gradient(
      circle,
      rgba(113, 81, 95, 1) 81%,
      rgba(0, 0, 0, 1) 100%
    );
    @apply flex
    justify-center
    items-center
    h-[100px]
    border-[2px]
    border-black;
  }
  &:nth-child(3),
  &:nth-child(5),
  &:nth-child(9) {
    .col-bg {
      @extend .-blinking;
    }
  }
}
.ball {
  /* transform: translate(-50%, -50%); */
  @apply absolute
  origin-center
  z-[1]
  top-[50%]
  left-[50%]
  w-[30px]
  h-[30px]
  bg-[#A5F12B]
  rounded-[50%];
}
</style>
