<script setup>
import Button from './Components/Button.vue';
import Header from './Components/Header.vue';
import Card from './Components/Card.vue';
import { ref } from 'vue';

const gameState = ref(false);
const gameScore = ref(100);
const data = ref([]);

async function getData() {
  const res = await fetch('http://localhost:8080/api/random-words');
  const json = await res.json();

  if (!res) {
    data.value = null;
    return [];
  }

  data.value = json.map((item, index) => ({
    word: item.word,
    translation: item.translation,
    status: 'pending',
    state: 'closed',
    correctAnswer: Math.random() > 0.5 ? 'success' : 'fail',
    cardNumber: String(index + 1)
  }));
}

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
        <Button @click="gameState = true, getData()">{{ 'Начать игру' }}</Button >
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
      <Button @click="gameState = false">{{ 'Начать заново' }}</Button >
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
