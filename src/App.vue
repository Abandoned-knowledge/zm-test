<script setup lang="ts">
import { ref, useTemplateRef, watch } from "vue";

import LogoIcon from "@icons/logo.svg";
import VButton from "@components/VButton.vue";
import VWheel from "@components/VWheel.vue";
import VDialog from "@components/VDialog.vue";
import { CALL_DIALOG_DELAY_IN_MS } from "./constants";

const isPrizeTaken = ref(true);
const isSpinnig = ref(false);
const isDialogOpen = ref(false);
const wheelRef = useTemplateRef("wheel");

watch(isSpinnig, (isSpin) => {
  if (isSpin) return;

  setTimeout(() => {
    isDialogOpen.value = true;
    wheelRef.value?.resetWheelRotate();
  }, CALL_DIALOG_DELAY_IN_MS);
});

function onClick() {
  isPrizeTaken.value = false;
  wheelRef.value?.spinWheel(7);
}

const prizeRef = ref<number | undefined>(0);
</script>

<template>
  <main class="main">
    <LogoIcon />
    <VWheel
      ref="wheel"
      @spin-end="(prize) => (prizeRef = prize)"
      v-model="isSpinnig"
    />

    <VButton :disabled="isSpinnig || !isPrizeTaken" @click="onClick">
      Крути
    </VButton>
  </main>

  <VDialog
    @close="isPrizeTaken = true"
    :prize="prizeRef"
    v-model="isDialogOpen"
  />
</template>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  height: 100dvh;
  width: fit-content;
  margin-inline: auto;
  padding-top: clamp(2.5rem, 1.878vw + 2.06rem, 3.75rem);
  padding-bottom: clamp(3.25rem, 1.127vw + 2.986rem, 4rem);
  position: relative;

  .button {
    width: 80%;
  }

  &::before,
  &::after {
    content: "";
    position: fixed;
    width: 1200px;
    aspect-ratio: 2/1;
    margin-inline: auto;
    border-radius: 100%;
    filter: blur(120px);
    z-index: -10;
  }

  &::before {
    background-color: rgba(35, 132, 166, 0.5);
    top: -10%;
  }

  &::after {
    background-color: rgba(83, 19, 132, 0.5);
    bottom: -15%;
  }
}
</style>
