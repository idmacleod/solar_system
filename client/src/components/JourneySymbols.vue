<template>
  <div id="journey-symbols">
    <h1><span class="sym">⨁</span></h1>
  </div>
</template>

<script>
export default {
  name: 'journey-symbols',
  props: ['symbols']
}
</script>

<style>
#journey-symbols h1 {
  font-family: 'Nixie One';
  background: black;
  color: white;
  margin: 0 0 10px 0;
  padding: 10px;
}
</style>