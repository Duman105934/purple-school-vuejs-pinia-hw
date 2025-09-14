<script setup >

import Button from './Components/Button.vue';
import Header from './Components/Header.vue';
import Card from './Components/Card.vue';
import { reactive } from 'vue';

const gameState = reactive(true);
const gameBtnText = !gameState ? 'Начать игру' : 'Начать заново';

const data = reactive({
  gameScore: 100,
  cardNumber: '02',
  englishText: 'black cat',
  translatedText: 'черный кот',
  correctAnswer: 'success',
  isAnswerCorrect: null,
  cardState: 'flip', // "flip" | "revealed" | "completed"
});

function onEnter() {
  if (data.cardState === 'flip') {
    data.cardState = 'revealed';
  }
}

function onLeave() {
  if (data.cardState !== 'completed') {
    data.cardState = 'flip';
  }
}

function checkingUserAnswer(userAnswer) {
  if (userAnswer === data.correctAnswer) {
    data.isAnswerCorrect = true;
  } else if (userAnswer !== data.correctAnswer) {
    data.isAnswerCorrect = false;
  }
  data.cardState = 'completed';
}

</script >

<template >

  <div class="layout" >
    <!--Заголовок игры-->
    <div class="header" >
      <Header :game-score="data.gameScore" />
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
