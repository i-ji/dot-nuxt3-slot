<template>
  <div
    class="bg-gray-200 w-[350px] p-5 border-4 border-white rounded-2xl my-4 mx-auto flex justify-between"
  >
    <div>
      <img
        :src="image1"
        alt=""
        class="w-[90px] h-[110px] mb-2"
        :class="{ unmatch: isUnmatched1 }"
      />
      <StopButton @stop="stop1" :stopState="stopState1"></StopButton>
    </div>
    <div>
      <img
        :src="image2"
        alt=""
        class="w-[90px] h-[110px] mb-2"
        :class="{ unmatch: isUnmatched2 }"
      />
      <StopButton @stop="stop2" :stopState="stopState2"></StopButton>
    </div>
    <div>
      <img
        :src="image3"
        alt=""
        class="w-[90px] h-[110px] mb-2"
        :class="{ unmatch: isUnmatched3 }"
      />
      <StopButton @stop="stop3" :stopState="stopState3"></StopButton>
    </div>
  </div>
</template>

<style>
.unmatch {
  opacity: 0.5;
}
</style>

<script setup lang="ts">
const props = defineProps([
  "image1",
  "image2",
  "image3",
  "isUnmatched1",
  "isUnmatched2",
  "isUnmatched3",
  "stopState1",
  "stopState2",
  "stopState3",
]);
const emits = defineEmits(["stop1", "stop2", "stop3"]);
const stop1 = () => {
  emits("stop1");
};
const stop2 = () => {
  emits("stop2");
};
const stop3 = () => {
  emits("stop3");
};
</script>
