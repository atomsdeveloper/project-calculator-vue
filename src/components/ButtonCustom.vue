<template>
  <button class="button" :class="{ double, triple, operation }" @click="$emit('onClick', label)">
    {{ label }}
  </button>
</template>

<script>
export default {
  props: {
    label: {},
    double: {type: Boolean},
    triple: {type: Boolean},
    operation: {type: Boolean}
  }
}
</script>

<style>
:root {
  --bg-button: #f0f0f0;
  --border-button: solid 1px #888
}

.button {
  font-size: 1.4rem;
  background-color: var(--bg-button);
  border: none;
  border-right: var(--border-button);
  border-bottom: var(--border-button);
  outline: none;
}

.button:active {
  background-color: #ccc;
}

.button.double {
  grid-column: span 2;
}

.button.triple {
  grid-column: span 3;
}

.button.operation {
  background-color: #fa8231;
  color: aliceblue
}

.button.operation {
  background-color: #fa8231cc;
}
</style>