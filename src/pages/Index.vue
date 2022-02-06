<template>
  <div class="container" v-touch-repeat:0:300:200.39.37="handleKeyPress">
    <div class="container-bg q-pa-md" style="background-image: url('ac-bg.png')">
    </div>
    <div class="q-pa-md flex-center flex relative-position">
      <div class="absolute-top q-ma-md">
        <span class="text-bold text-h6">{{ index }}</span> / {{ count }}
        <q-linear-progress stripe size="18px" :value="index/count"/>
      </div>
      <div style="max-width: 600px">

        <p class="text-h4" v-html="computeQuestion.stem"></p>
        <div v-for="(option, index) in computeQuestion.options" :key="option">
          <span
            :class="computeQuestion.answer.indexOf(index) !== -1 ? 'text-green-8 text-bold display-inline': 'display-inline'"
            v-html="option"></span>
        </div>
        <div class="text-grey-8" v-html="computeQuestion.analysis"></div>
        <div class="full-width absolute-bottom flex justify-between q-pa-md">
          <q-btn outline @click="handleLeft" label="left"></q-btn>
          <q-btn outline @click="handleRight" label="right"></q-btn>
        </div>
      </div>
    </div>

  </div>
</template>

<script setup lang="ts">
import question from './questions.json'
import {computed, ref} from 'vue';

const index = ref(0)
const count = question.list.length;
const computeQuestion = computed(() => {
  if (index.value >= question.list.length) {
    return question.list.length - 1;
  }
  return question.list[index.value]
})
// eslint-disable-next-line @typescript-eslint/no-unsafe-member-access
function handleLeft() {
  if (index.value === 0) {
    index.value = question.list.length;
  } else {
    index.value = index.value - 1;
  }
}

function handleRight() {
  if (index.value === question.list.length) {
    index.value = 0;
  } else {
    index.value = index.value + 1;
  }
}

function handleKeyPress(key: unknown) {
  // eslint-disable-next-line @typescript-eslint/no-unsafe-member-access
  if (key.keyCode === 39) {
    handleRight()
    // eslint-disable-next-line @typescript-eslint/no-unsafe-member-access
  } else if (key.keyCode === 37) {
    handleLeft()
  }
}
</script>

<style lang='scss' scoped>
.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-column-gap: 0px;
  grid-row-gap: 20px;
  justify-items: stretch;
  align-items: stretch;
  height: 100%;
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;

  &-title {
    background: #810CCF;
    background: -webkit-linear-gradient(to right, #810CCF 0%, #CFA6A6 100%);
    background: -moz-linear-gradient(to right, #810CCF 0%, #CFA6A6 100%);
    background: linear-gradient(to right, #810CCF 0%, #CFA6A6 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  & > div {
    height: 100%;
  }

  &-bg {
    background-size: cover;
  }

  &-login {
    background: white !important;
    display: flex;
    justify-content: center;
    align-content: center;
    align-items: center;

    &-box {
      width: 350px;
    }
  }
}

</style>
