<template>
  <button
    class="w-[90px] h-8 bg-[#ef454a] shadow-[0_4px_0_#d1483d] rounded-2xl leading-8 text-sm text-white"
    @click="stop"
    :disabled="stopState"
  >
    STOP
  </button>
</template>

<style>
button:disabled {
  opacity: 0.5;
}
</style>

<script setup lang="ts">
const props = defineProps(["stopState"]);
const emits = defineEmits(["stop"]);
const stop = () => {
  emits("stop");
};
</script>
