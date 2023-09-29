<template>
  <div class="font-bold mx-auto">
    <Panel
      :image1="image1"
      :image2="image2"
      :image3="image3"
      @stop1="stop1"
      @stop2="stop2"
      @stop3="stop3"
      :isUnmatched1="isUnmatched1"
      :isUnmatched2="isUnmatched2"
      :isUnmatched3="isUnmatched3"
      :stopState1="stopState1"
      :stopState2="stopState2"
      :stopState3="stopState3"
    ></Panel>
    <Spin @spin="spin" :spinState="spinState"></Spin>
  </div>
</template>

<script setup lang="ts">
// imageにURLを付与
let image1 = ref<string>("");
let image2 = ref<string>("");
let image3 = ref<string>("");

image1.value = getRandomImage();
image2.value = getRandomImage();
image3.value = getRandomImage();

function getRandomImage(): string {
  const images = ref<string[]>([
    "../img/seven.png",
    "../img/bell.png",
    "../img/cherry.png",
  ]);
  return images.value[Math.floor(Math.random() * images.value.length)];
}

// スロットを回す
let timeoutId1: NodeJS.Timeout;
let timeoutId2: NodeJS.Timeout;
let timeoutId3: NodeJS.Timeout;

function spinSlot1() {
  image1.value = getRandomImage();
  timeoutId1 = setTimeout(() => {
    spinSlot1();
  }, 50);
}

function spinSlot2() {
  image2.value = getRandomImage();
  timeoutId2 = setTimeout(() => {
    spinSlot2();
  }, 50);
}

function spinSlot3() {
  image3.value = getRandomImage();
  timeoutId3 = setTimeout(() => {
    spinSlot3();
  }, 50);
}

let spinState = ref<boolean>(false);

const spin = () => {
  spinState.value = true;
  panelsLeft.value = 3;
  isUnmatched1.value = false;
  isUnmatched2.value = false;
  isUnmatched3.value = false;
  stopState1.value = false;
  stopState2.value = false;
  stopState3.value = false;
  spinSlot1();
  spinSlot2();
  spinSlot3();
};

// スロットを止める
let panelsLeft = ref<number>(3);
let isUnmatched1 = ref<boolean>(false);
let isUnmatched2 = ref<boolean>(false);
let isUnmatched3 = ref<boolean>(false);
let stopState1 = ref<boolean>(true);
let stopState2 = ref<boolean>(true);
let stopState3 = ref<boolean>(true);

const stop1 = () => {
  clearTimeout(timeoutId1);
  stopState1.value = true;
  panelsLeft.value--;
  checkResult();
};

const stop2 = () => {
  clearTimeout(timeoutId2);
  stopState2.value = true;
  panelsLeft.value--;
  checkResult();
};
const stop3 = () => {
  clearTimeout(timeoutId3);
  stopState3.value = true;
  panelsLeft.value--;
  checkResult();
};

function checkResult() {
  if (panelsLeft.value === 0) {
    if (image1.value !== image2.value && image1.value !== image3.value) {
      isUnmatched1.value = true;
    }

    if (image2.value !== image1.value && image2.value !== image3.value) {
      isUnmatched2.value = true;
    }

    if (image3.value !== image2.value && image3.value !== image1.value) {
      isUnmatched3.value = true;
    }

    spinState.value = false;
  }
}
</script>
