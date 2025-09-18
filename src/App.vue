<script setup >

import Button from './Components/Button.vue';
import Header from './Components/Header.vue';
import Card from './Components/Card.vue';
import { ref } from 'vue';

const gameState = ref(true);
const gameBtnText = !gameState.value ? 'Начать игру' : 'Начать заново';

const gameScore = ref(100);

const data = ref(
    [
      {
        word: 'black cat',
        translation: 'черный кот',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'success',
        cardNumber: '01'
      },
      {
        word: 'white dog',
        translation: 'белая собака',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'fail',
        cardNumber: '02'
      },
      {
        word: 'green apple',
        translation: 'зелёное яблоко',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'success',
        cardNumber: '03'
      },
      {
        word: 'red car',
        translation: 'красная машина',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'fail',
        cardNumber: '04'
      },
      {
        word: 'blue sky',
        translation: 'голубое небо',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'success',
        cardNumber: '05'
      },
      {
        word: 'yellow sun',
        translation: 'жёлтое солнце',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'fail',
        cardNumber: '06'
      },
      {
        word: 'brown bear',
        translation: 'бурый медведь',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'success',
        cardNumber: '07'
      },
      {
        word: 'orange juice',
        translation: 'апельсиновый сок',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'fail',
        cardNumber: '08'
      },
      {
        word: 'pink flower',
        translation: 'розовый цветок',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'success',
        cardNumber: '09'
      },
      {
        word: 'gray mouse',
        translation: 'серая мышь',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'fail',
        cardNumber: '10'
      },
      {
        word: 'long road',
        translation: 'длинная дорога',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'success',
        cardNumber: '11'
      },
      {
        word: 'big house',
        translation: 'большой дом',
        status: 'pending',
        state: 'closed',
        correctAnswer: 'fail',
        cardNumber: '12'
      },
    ]
);

function onEnter(item) {
  if (item.state === 'closed') {
    item.state = 'opened';
  }
}

function onLeave(item) {
  if (item.state === 'opened') {
    item.state = 'closed';
  }
}

function checkingUserAnswer(item, userAnswer) {
  if (userAnswer === item.correctAnswer) {
    item.status = 'success';
  } else if (userAnswer !== item.correctAnswer) {
    item.status = 'fail';
  }
  item.state = 'closed';
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
            v-for="item in data" :key="item.cardNumber"
            v-bind="item"
            @user-select-answer="checkingUserAnswer(item, $event)"
            @mouseenter="onEnter(item)"
            @mouseleave="onLeave(item)"
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
