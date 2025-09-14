<script setup >
import HeartIcon from '../icons/HeartIcon.vue';

const {gameScore} = defineProps({
  gameScore: Number
});
</script >

<template >
  <div class="header__right-score" >
    {{ gameScore }}
  </div >
  <HeartIcon />
</template >

<style scoped >

.header__right-score {
  margin-right: 10px;
  font-size: 16px;
  font-style: normal;
  font-weight: 700;
  line-height: 24px; /* 150% */
  color: var(--color-button);
}

</style >