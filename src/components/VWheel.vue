<script setup lang="ts">
const wheelSections = [50, "пусто", 100, "повтор", 150, "пусто", 300, "повтор"];
</script>

<template>
  <div class="wheel-container">
    <ul class="wheel">
      <li
        class="wheel__section"
        v-for="(content, index) in wheelSections"
        :key="index"
      >
        <span class="wheel__text text-gradient">{{ content }}</span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.wheel-container {
  width: clamp(18.75rem, 42.254vw + 8.847rem, 46.875rem);
  aspect-ratio: 1;
  background: url("/src/assets/svg/wheel-border.svg") no-repeat center/ 100%;
  position: relative;
  box-shadow: 0px 0px 50px #0e1155;
  border-radius: 50%;

  &::before,
  &::after {
    content: "";
    position: absolute;
  }

  &::before {
    background: url("/src/assets/svg/wheel-arrow.svg") no-repeat center;
    inset-inline: 0;
    top: -15%;
    margin-inline: auto;
    background-size: contain;
    height: 35%;
    aspect-ratio: 1;
  }

  &::after {
    inset: 0;
    margin: auto;
    background: url("/src/assets/svg/wheel-center.svg") no-repeat center / 30%;
    z-index: 10;
  }

  &:hover .wheel {
    rotate: 45deg;
  }
}

.wheel {
  height: 100%;
  width: 100%;
  list-style-type: none;
  padding-left: 0;
  display: flex;
  justify-content: center;
  transition: 1s ease-in-out;
  position: relative;
  margin: 0;
  z-index: -5;

  &::after {
    content: "";
    position: absolute;
    inset: 0;
    margin: auto;
    background: url("/src/assets/svg/wheel-center-divier.svg") no-repeat center/
      90%;
  }
}

.wheel__section {
  --section-rotate: 45deg;

  display: flex;
  justify-content: center;
  padding-top: 15%;
  position: absolute;
  text-transform: uppercase;
  background-repeat: no-repeat;
  background-size: contain;
  height: 50%;
  aspect-ratio: 3/4;
  top: 0;
  inset-inline: auto;
  z-index: -10;
  transform-origin: bottom;

  &:nth-child(even) {
    background-image: url("/src/assets/svg/wheel-section-light.svg");
  }

  &:nth-child(odd) {
    background-image: url("/src/assets/svg/wheel-section-dark.svg");
  }

  &:nth-child(1) {
    rotate: calc(var(--section-rotate) * 0);
  }

  &:nth-child(2) {
    rotate: calc(var(--section-rotate) * 1);
  }

  &:nth-child(3) {
    rotate: calc(var(--section-rotate) * 2);
  }

  &:nth-child(4) {
    rotate: calc(var(--section-rotate) * 3);
  }

  &:nth-child(5) {
    rotate: calc(var(--section-rotate) * 4);
  }

  &:nth-child(6) {
    rotate: calc(var(--section-rotate) * 5);
  }

  &:nth-child(7) {
    rotate: calc(var(--section-rotate) * 6);
  }

  &:nth-child(8) {
    rotate: calc(var(--section-rotate) * 7);
  }
}

.wheel__text {
  -webkit-text-stroke-width: 2px;
}
</style>
