<script setup>
import { ref } from 'vue';

const spin = ref([]);
const isDead = ref(false);

function prepareBarrel() {
  let barrel = [];
  for (let i = 0; i < 6; i++) {
    if (barrel.length === 0) {
      barrel.push(false);
    } else {
      if (barrel.includes(true)) {
        barrel.push(false);
      } else {
        if (Math.random() < 0.2) {
          barrel.push(true);
        } else {
          barrel.push(false);
        }
      }
    }
  }

  if (!barrel.includes(true)) {
    barrel = prepareBarrel();
  }

  return barrel;
}

function roll() {
  if (isDead.value) {
    spin.value = prepareBarrel();
    isDead.value = false;
  }
  if (spin.value.length === 0) {
    spin.value = prepareBarrel();
  }

  let current = spin.value[0];
  spin.value = spin.value.slice(1, spin.value.length);

  if (current === true) {
    isDead.value = true;
  }
  console.log(spin.value, current, isDead.value);
}
</script>

<template>
  <p>
    <button :onclick="roll">Spin</button>
  </p>
  <p>
    {{ isDead ? 'You die' : 'You live' }}
  </p>
  <button v-for="(c, i) in spin" v:key="i + 1">o</button>
</template>

<style></style>
