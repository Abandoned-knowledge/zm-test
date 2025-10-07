<script setup lang="ts">
const props = defineProps<{
  disabled?: boolean;
}>();
</script>

<template>
  <button class="button" :disabled="props.disabled">
    <span class="button__text text-gradient">
      <template v-if="props.disabled">Подожди...</template>
      <slot v-else></slot>
    </span>
  </button>
</template>

<style scoped>
.button {
  background-image: var(--gradient-accent);
  padding: clamp(0.75rem, 0.376vw + 0.662rem, 1rem);
  border-radius: 1000px;
  border: none;
  box-shadow: inset 0px -4px 2.7px rgba(0, 0, 0, 0.2),
    inset 0px 2.7px 2.7px rgba(255, 255, 255, 0.5),
    0px 4px 8px rgba(27, 26, 72, 0.5);
  text-transform: uppercase;
  font-size: var(--text-button);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: box-shadow 0.15s ease-in-out;

  @media screen and (hover: hover) {
    &:hover {
      box-shadow: inset 0px -6px 4px rgba(0, 0, 0, 0.2),
        inset 0px 4px 4px rgba(255, 255, 255, 0.5),
        0px 6px 12px rgba(38, 108, 154, 1);
    }
  }

  &:active {
    box-shadow: none;
  }

  &:disabled {
    cursor: not-allowed;
    background-image: var(--gradient-disabled);
    box-shadow: none;
  }
}

.button__text {
  -webkit-text-stroke-width: 2px;
}
</style>
