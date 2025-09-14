<script setup ></script >

<template >
  <button class="button" >
    <slot />
  </button >
</template >

<style scoped >

.button {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  width: 335px;
  padding: 16px 10px;
  gap: 10px;
  border: none;
  border-radius: 100px;
  text-align: center;
  font-size: 24px;
  font-style: normal;
  font-weight: 400;
  line-height: 36px;
  color: var(--color-text-button);
  background: var(--color-button);
  cursor: pointer;
}

.button:hover {
  background: var(--color-bg-hover);
}
</style >