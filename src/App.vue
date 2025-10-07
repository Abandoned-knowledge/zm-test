<script setup lang="ts">
import { ref } from "vue";

import LogoIcon from "@icons/logo.svg";
import VButton from "@components/VButton.vue";
import VWheel from "@components/VWheel.vue";
import VDialog from "@components/VDialog.vue";

const isDialogOpen = ref(false);
</script>

<template>
  <main class="main">
    <LogoIcon />
    <VWheel />
    <VButton @click="isDialogOpen = true">Крути</VButton>
  </main>

  <VDialog v-model="isDialogOpen" />
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
