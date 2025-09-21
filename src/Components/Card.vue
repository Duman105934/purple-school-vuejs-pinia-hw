<script setup>

import SuccessIcon from '../icons/SuccessIcon.vue';
import FailIcon from '../icons/FailIcon.vue';

const iconSizeL = 36;
const iconSizeS = 24;
const cardFlipText = 'ПЕРЕВЕНУТЬ';
const cardCompletedText = 'ЗАВЕРШЕНО';

const props = defineProps({
  word: String,
  translation: String,
  status: String, // "success" | "pending" | "fail"
  state: String, // "closed" | "opened"
  correctAnswer: String,
  cardNumber: String,
});

const emit = defineEmits(['userSelectAnswer']);

function userSelectedAnswer(userAnswer) {
  emit('userSelectAnswer', userAnswer);
}

</script >

<template >

  <div class="substrate" >

    <!--Нумерация карточки-->
    <div class="substrate__number" >{{ props.cardNumber }}</div >

    <!--Текст карточки-->
    <div class="card" >
      <div v-if="props.state === 'closed' && props.status === 'pending'" class="card__text" >{{ props.word }}</div >
      <div v-else class="card__text" >{{ props.translation }}</div >
    </div >

    <!--Результат игры после ответа пользователя-->
    <div class="substrate__top-icons" >
      <div v-if="props.status === 'pending'" ></div >
      <div v-else-if="props.status ==='success'" class="substrate__top-icons top-icon__success" >
        <SuccessIcon :icon-size="iconSizeL" />
      </div >
      <div v-else class="substrate__top-icons top-icon__fail" >
        <FailIcon :icon-size="iconSizeL" />
      </div >
    </div >

    <!--Выбор ответа пользователя и состояние карты-->
    <div class="substrate__bottom" >
      <div v-if="props.state === 'closed' && props.status === 'pending'" class=" substrate__bottom-text" >{{ cardFlipText }}</div >
      <div v-else-if="props.state === 'opened' && props.status === 'pending'" class="substrate__bottom-icons" >
        <SuccessIcon :icon-size="iconSizeS" @click="userSelectedAnswer('success')" />
        <FailIcon :icon-size="iconSizeS" @click="userSelectedAnswer('fail')" />
      </div >
      <div v-else class=" substrate__bottom-text" >{{ cardCompletedText }}</div >
    </div >

  </div >

</template >

<style scoped >

.substrate {
  position: relative;
  width: var(--card-width);
  height: var(--card-height);
  padding: 28px 19px;
  border-radius: 16px;
  box-shadow: 0 0 16px 0 rgba(0, 0, 0, 0.10);
  background: var(--color-bg-card);
  cursor: pointer;
}

.card {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 212px;
  height: 320px;
  border-radius: 12px;
  border: 1px solid var(--color-border-card);
  background: var(--color-bg-card);
}

.card__text {
  width: 180px;
  text-align: center;
}

.substrate__bottom {
  position: absolute;
  left: 80px;
  bottom: 11px;
}

.substrate__bottom-icons {
  display: inline-flex;
  justify-content: space-between;
  align-items: center;
  width: 97px;
  height: 18px;
  gap: 10px;
  padding: 0 4px;
  bottom: 19px;
  font-size: 24px;
  background-color: var(--color-bg-card);
}

.substrate__top-icons {
  background-color: var(--color-bg-card);
}

.top-icon__success {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 6px;
}

.top-icon__fail {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: 6px;
}

.substrate__number {
  position: absolute;
  top: 20px;
  left: 35px;
  text-align: center;
  font-size: 14px;
  font-style: normal;
  font-weight: 400;
  line-height: 120%;
  background-color: var(--color-bg-card);
  color: var(--color-text-primary);
}

.substrate__bottom-text {
  position: absolute;
  bottom: 8px;
  font-size: 12px;
  font-style: normal;
  font-weight: 700;
  line-height: 18px; /* 150% */
  letter-spacing: 2px;
  background-color: var(--color-bg-card);
  color: var(--color-text-primary-hover);
}

</style >