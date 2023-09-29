<template>
  <div class="text-center">
    <button
      class="w-[280px] h-9 bg-[#3498db] shadow-[0_4px_0_#2880b9] rounded-[18px] leading-9 text-white"
      @click="spin"
      :disabled="spinState"
    >
      SPIN
    </button>
  </div>
</template>

<style>
button:disabled {
  opacity: 0.5;
}
</style>

<script setup lang="ts">
const props = defineProps(["spinState"]);
const emits = defineEmits(["spin"]);
const spin = () => {
  emits("spin");
};
</script>
