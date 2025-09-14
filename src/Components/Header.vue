<script setup >

import Score from './Score.vue';

const {gameScore} = defineProps({
  gameScore: Number
});

</script >

<template >

  <div class="header" >
    <!--Наименование игры-->
    <div class="header__left" >ЗАПОМНИ СЛОВО</div >

    <!--Количество очков и иконка-->
    <div class="header__right" >
      <Score :game-score="gameScore"/>
    </div >
  </div >
</template >

<style scoped >

.header {
  display: flex;
  height: var(--header-height);
  padding: 0 16px;
  justify-content: space-between;
  align-items: center;
  align-content: center;
}

.header__left {
  margin: 0;
  font-size: 16px;
  font-style: normal;
  font-weight: 700;
  line-height: 24px; /* 150% */
  letter-spacing: 2px;
  color: var(--color-text-primary-hover);
}

.header__right {
  display: flex;
  text-align: center;
  margin: 0;
  padding: 12px 24px;
  border-radius: 36px;
  background: var(--color-border-card);
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.15);
}


</style >