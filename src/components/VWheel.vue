<script setup lang="ts">
import { ref } from "vue";

import {
  DEFAULT_WHEEL_SPINS,
  SPIN_DURATION_IN_SECONDS,
  WHEEL_RADIUS,
} from "@constants/index";

const wheelSections = [
  { label: "50", prize: 50 },
  { label: "пусто", prize: 0 },
  { label: "100", prize: 100 },
  { label: "повтор", prize: 0 },
  { label: "150", prize: 150 },
  { label: "пусто", prize: 0 },
  { label: "300", prize: 300 },
  { label: "повтор", prize: 0 },
];

const sectionDegrees = WHEEL_RADIUS / wheelSections.length;

const isSpinningModel = defineModel();

function spinWheel(finalPosition: number) {
  isSpinningModel.value = true;

  const sectionIndex = finalPosition - 1;

  spinDegrees.value +=
    WHEEL_RADIUS * DEFAULT_WHEEL_SPINS + sectionIndex * sectionDegrees;

  emit("spin-end", wheelSections[sectionIndex]?.prize);

  setTimeout(
    () => (isSpinningModel.value = false),
    SPIN_DURATION_IN_SECONDS * 1000
  );
}

const resetWheelRotate = () => (spinDegrees.value = 0);

const spinDegrees = ref(0);

defineExpose({
  spinWheel,
  resetWheelRotate,
});

const emit = defineEmits<{
  "spin-end": [prize?: number];
}>();
</script>

<template>
  <div class="wheel-container">
    <ul class="wheel" :class="{ 'wheel--animated': isSpinningModel }">
      <li
        class="wheel__section"
        v-for="(section, index) in wheelSections"
        :key="index"
      >
        <span class="wheel__text text-gradient">{{ section.label }}</span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.wheel-container {
  height: clamp(20.313rem, 25.822vw + 14.261rem, 37.5rem);
  aspect-ratio: 1;
  background: url("/src/assets/svg/wheel-border.svg") no-repeat center/ 101%;
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
}

.wheel {
  height: 100%;
  width: 100%;
  list-style-type: none;
  padding-left: 0;
  display: flex;
  justify-content: center;
  position: relative;
  margin: 0;
  z-index: -5;
  rotate: calc(v-bind(spinDegrees) * -1deg);

  &::after {
    content: "";
    position: absolute;
    inset: 0;
    margin: auto;
    background: url("/src/assets/svg/wheel-center-divier.svg") no-repeat center/
      90%;
  }
}

.wheel--animated {
  transition: calc(v-bind(SPIN_DURATION_IN_SECONDS) * 1s) ease-in-out;
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
