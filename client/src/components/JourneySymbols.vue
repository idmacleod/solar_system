<template>
  <div id="journey-symbols">
    <h1>
      <span class="sym">⨁</span>
      <span v-for="(symbol, index) in symbols" :key="index" :symbol="symbol">
        <span>  ~  </span><span class="sym">{{ symbol }}</span>
      </span>
    </h1>
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
  padding: 10px 20px;
}

.sym {
  display: inline-block;
  animation: 5s linear infinite spin;
}

@keyframes spin {
  from {
      transform: rotate(0deg);
  }
  to {
      transform: rotate(360deg);
  }
}
</style>