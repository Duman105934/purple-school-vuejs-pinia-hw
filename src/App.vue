<script setup >

import Button from './Components/Button.vue';
import Header from './Components/Header.vue';
import Card from './Components/Card.vue';
import { ref } from 'vue';

const gameState = ref(true);
const gameBtnText = !gameState.value ? 'Начать игру' : 'Начать заново';

const gameScore = ref(50)
const data = ref({
  word: 'black cat',
  translation: 'черный кот',
  status: 'pending', // "success" | "pending" | "fail"
  state: 'closed', // "closed" | "opened"
  correctAnswer: 'success',
  cardNumber: '02',
});

function onEnter() {
  if (data.value.state === 'closed') {
    data.value.state = 'opened';
  }
}

function onLeave() {
  if (data.value.state === 'opened') {
    data.value.state = 'closed';
  }
}

function checkingUserAnswer(userAnswer) {
  if (userAnswer === data.value.correctAnswer) {
    data.value.status = 'success';
  } else if (userAnswer !== data.value.correctAnswer) {
    data.value.status = 'fail';
  }
  data.value.state = 'closed';
}

</script >

<template >

  <div class="layout" >
    <!--Заголовок игры-->
    <div class="header" >
      <Header :game-score="gameScore" />
    </div >

    <!--Основной блок игры-->
    <div class="main" >
      <div v-if="!gameState" class="center" >
        <Button >{{ gameBtnText }}</Button >
      </div >
      <div v-else class="cards" >
        <Card
            v-bind="data"
            @user-select-answer="checkingUserAnswer"
            @mouseenter="onEnter"
            @mouseleave="onLeave"
        />
      </div >
    </div >

    <!--Кнопка запуска/перезапуска игры-->
    <div v-if="gameState" class="footer" >
      <Button >{{ gameBtnText }}</Button >
    </div >
  </div >

</template >

<style scoped >

.layout {
  display: grid;
  grid-template-rows: var(--header-height, auto) 1fr auto;
  max-width: var(--max-width);
  min-width: var(--min-width);
  height: min(100%, var(--max-height));
  margin: 0 auto;
}

.main {
  max-height: calc(var(--max-height) - var(--header-height));
  padding: 49px 66px;
  justify-content: start;
  align-content: flex-start;
}

.center {
  display: flex;
  justify-content: center;
  align-items: center;

}

.cards {
  display: grid;
  grid-template-columns: repeat(4, var(--card-width));
  grid-auto-rows: var(--card-height);
  column-gap: var(--gap);
  row-gap: var(--gap);
  justify-content: center;
  align-content: start;
}

.footer {
  display: flex;
  justify-content: center;
  margin: 101px auto 66px auto;
}

</style >
