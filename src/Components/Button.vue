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
  width: 335px;
  padding: 16px 10px;
  align-items: flex-start;
  gap: 10px;
  border: none;
  cursor: pointer;

  border-radius: 100px;
  background: var(--color-button);
  color: var(--color-text-button);

  text-align: center;
  font-size: 24px;
  font-style: normal;
  font-weight: 400;
  line-height: 36px;
}

.button:hover {
  background: var(--color-bg-hover);
}
</style >