<template>
  <div class="display">
    {{ value }}
  </div>
</template>

<script>
export default {
  props: ["value"]
}
</script>

<style>
.display {
  grid-column: span 4;

  display: flex;
  align-items: center;
  justify-content: flex-end;
  
  padding: 20px;
  overflow: hidden;
  
  font-size: 2.2rem;
  background-color: #0004;
}
</style>