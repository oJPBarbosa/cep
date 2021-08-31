<template>
  <div id="app">
    <Consultor />
  </div>
</template>

<script>
import Consultor from "./components/Consultor.vue";

export default {
  name: "App",
  components: {
    Consultor,
  },
};
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  height: 100%;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;

  height: 100%;

  background: var(--body-bg-color);
}

@media (prefers-color-scheme: dark) {
  :root {
    --body-bg-color: #202029;
  }
}

@media (prefers-color-scheme: light) {
  :root {
    --body-bg-color: #ffffff;
  }
}

@media (prefers-color-scheme: no-prefence) {
  :root {
    --body-bg-color: #ffffff;
  }
}
</style>
