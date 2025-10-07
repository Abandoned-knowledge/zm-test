<script setup lang="ts">
import { useTemplateRef, watch } from "vue";
import VButton from "./VButton.vue";

const props = defineProps<{
  prize?: number;
}>();

const dialog = useTemplateRef("dialog");
const isOpenModel = defineModel<boolean>();

watch(isOpenModel, (isOpen) => {
  isOpen ? dialog.value?.showModal() : dialog.value?.close();
});
</script>

<template>
  <dialog class="modal" ref="dialog">
    <div class="modal__content">
      <h1 class="text-gradient">
        ТЫ МОЛОДЕЦ!
        <br />
        <br />
        <span class="text-accent">ВОТ ТВОИ {{ props.prize }}</span>
      </h1>
      <VButton @click="isOpenModel = false">забрать</VButton>
    </div>
  </dialog>
</template>

<style scoped>
.modal {
  border: solid clamp(0.375rem, 0.282vw + 0.309rem, 0.563rem) transparent;
  border-radius: clamp(2.5rem, 1.878vw + 2.06rem, 3.75rem);
  background-image: linear-gradient(transparent, transparent),
    linear-gradient(137deg, #789cd2, #403ea6, #3e1e72);
  background-origin: border-box;
  background-clip: padding-box, border-box;
  padding: 0;
  width: max(350px, 500px);
  transition: all 0.3s ease-in-out allow-discrete;
  opacity: 0;
  transform: translateY(10%);

  &::backdrop {
    opacity: 1;
    background-color: transparent;
    transition: all 0.3s ease-in-out allow-discrete;
  }

  &:open {
    opacity: 1;
    transform: translateY(0);
  }

  &:open::backdrop {
    background-color: rgba(32, 10, 67, 0.7);
  }
}

.modal__content {
  background-image: linear-gradient(154deg, #5977c3 10%, #54268d 90%);
  padding: clamp(1.5rem, 1.502vw + 1.148rem, 2.5rem);
  display: flex;
  flex-direction: column;
  gap: clamp(3rem, 1.127vw + 2.736rem, 3.75rem);

  h1 {
    text-align: center;
    -webkit-text-stroke-width: 2px;
  }
}

@starting-style {
  .modal:open {
    opacity: 0;
    transform: translateY(10%);
  }

  .modal:open::backdrop {
    opacity: 0;
    background-color: transparent;
  }
}
</style>
