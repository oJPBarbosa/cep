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
@font-face {
  font-family: sf;
  src: url(./assets/font/sf.ttf);
}

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

  background: #0e1224;
}

#app {
  font-family: sf;

  text-align: left;

  color: #ffffff;
}
</style>
