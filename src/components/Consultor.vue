<template>
  <div id="consultant-container">
    <p id="header">Consulte qualquer CEP de uma forma simples e moderna.</p>
    <p id="input-label">Insira qualquer <b>CEP válido no Brasil</b>:</p>
      <div id="cep-input-container">
        <i class="fas fa-map-marker-alt"></i>
        <input
          type="text"
          autocomplete="off"
          placeholder="Seu melhor CEP"
          maxlength="9"
          v-model="cep_value"
          @keydown.enter="consult"
          @keydown.backspace="clear"
        />
      </div>
      <input
        type="button"
        id="consult-button"
        v-on:click="consult"
        value="Consultar CEP"
      />
      <div id="data-container">
        <p>Estado: {{ state_value }}</p>
        <p>Cidade: {{ city_value }}</p>
        <p>Bairro: {{ neighborhood_value }}</p>
        <p>Logradouro: {{ street_value }}</p>
      </div>
      <input type="button" id="clear-button" v-on:click="clear" value="Limpar" />
    <div id="footer">
      <p>
        Feito com 💙 por
        <a href="https://github.com/oJPBarbosa/consultor-de-cep" target="_blank" rel="noreferrer"
          >oJPBarbosa</a
        >.
      </p>
    </div>
  </div>
</template>

<script>
import cep from "cep-promise";

export default {
  name: "consultant-container",
  data() {
    return {
      cep_value: "",
      state_value: "",
      city_value: "",
      neighborhood_value: "",
      street_value: "",
    };
  },
  methods: {
    consult() {
      if (this.cep_value == '')
        return alert("Insira um CEP antes de consultá-lo.")

      else if (this.cep_value.length < 8)
        return alert("Insira um CEP válido!");

      cep(this.cep_value.replace("-", ""))
        .then((res) => {
          const json = JSON.parse(JSON.stringify(res));
          this.state_value = json["state"];
          this.city_value = json["city"];
          this.neighborhood_value = json["neighborhood"];
          this.street_value = json["street"];
        })
        .catch((err) => {
          this.clear();
          alert("Erro na consulta do CEP!");
          console.log(err);
        });

      document.getElementById("clear-button").style.display = "block";
      document.getElementById("data-container").style.display = "block";
    },
    clear() {
      this.cep_value = "";
      this.state_value = "";
      this.city_value = "";
      this.neighborhood_value = "";
      this.street_value = "";

      document.getElementById("clear-button").style.display = "none";
      document.getElementById("data-container").style.display = "none";
    },
  },
  watch: {
    cep_value: function (value) {
      this.cep_value = value.replace(/\D/g, "");
      this.cep_value = value.replace(/^(\d{5})(\d)/, "$1-$2");
    },
  },
};
</script>

<style>
@font-face {
  font-family: SF;
  src: url(../assets/fonts/sf.ttf);
}

#consultant-container {
  height: 100%;
  width: 20vw;
  min-width: 272px;

  display: flex;
  flex-direction: column;
  align-items: center;

  color: var(--general-text-color);

  font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", Roboto,
    "Helvetica Neue", Arial, sans-serif;

  text-align: left;
}

#header {
  margin-bottom: 30px;

  text-align: center;
  width: 120%;

  font-size: 32px;
  font-weight: 700;
}

input {
  border: none;
  outline: none;

  appearance: none;
}

#input-label {
  margin-bottom: 10px;
}

b {
  color: var(--bold-text-color);
}

#cep-input-container {
  height: 50px;
  width: 100%;

  color: var(--general-text-color);
  background: (general-text-color);

  outline: none;

  border: 1px solid var(--border-color);
  border-radius: 7.5px;

  font-size: 18px;

  padding: 5px;

  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
}

.fa-map-marker-alt {
  height: 32px;
  width: 32px;

  color: #757575;

  position: relative;
  top: 15%;
  left: 10px;
}

input[type="text"]  {
  height: 50px;
  width: 100%;

  color: var(--general-text-color);
  background: none;

  border: none;
  outline: none;

  font-size: 18px;

  margin-left: 10px;
}

::placeholder {
  color: #757575;

  font-size: 18px;
  font-weight: 100;
}

input[type="button"],
input[type="submit"] {
  height: 50px;
  width: 100%;

  color: #ffffff;
  cursor: pointer;
  font-size: 18px;

  margin-top: 10px;

  border-radius: 7.5px;

  transition: background 0.15s ease-in-out;
}

input[type="button"]:hover {
  transition: background 0.1s ease-in-out;
}

#consult-button {
  background: #0072f5;
  box-shadow: #0076ff60 0px 4px 14px 0px;
}

#consult-button:hover {
  background: #1983ff;
}

#data-container {
  height: 100%;
  width: 100%;

  font-family: SF;
  font-size: 18px;

  text-align: left;

  margin-top: 20px;

  display: none;
}

#data-container p {
  margin-top: 5px;
}

#clear-button {
  display: none;

  margin-top: 20px;

  background: #db3030;
  box-shadow: #db303060 0px 4px 14px 0px;
}

#clear-button:hover {
  background: #f04949;
}

#footer {
  height: 100%;

  font-family: SF;
  font-size: 18px;

  text-align: center;

  margin: 2.5vh;
}

#footer a {
  color: var(--footer-color);

  text-decoration: none;

  border-bottom: 2px solid var(--footer-border-color);

  transition: color 0.15s ease-out, border 0.15s ease-out;
}

#footer a:hover {
  color: #2965af;

  border-bottom-color: #2965af;

  transition: color 0.15s ease-in, border 0.15s ease-in;
}

@media screen and (max-width: 1350px) {
  #consultant-container {
    width: 30vw;
  }
}

@media screen and (max-width: 900px) {
  #consultant-container {
    width: 50vw;
  }
}

@media screen and (max-width: 550px) {
  #consultant-container {
    width: 75vw;
  }
  #header {
    font-size: 24px;
  }
}

@media screen and (max-width: 355px) {
  #consultant-container {
    width: 85vw;
  }
}

@media (prefers-color-scheme: dark) {
  :root {
    --general-text-color: #f0f0f0;
    --bold-text-color: #ffffff;
    --border-color: #fff8;
    --input-bg-color: #202029;
    --footer-border-color: #fff8;
    --footer-color: #55a2fa;
  }
}

@media (prefers-color-scheme: light) {
  :root {
    --general-text-color: #030303;
    --bold-text-color: #4e4e4e;
    --border-color: #0003;
    --input-bg-color: #ffffff;
    --footer-border-color: #0008;
    --footer-color: #0072f5;
  }
}

@media (prefers-color-scheme: no-prefence) {
  :root {
    --general-text-color: #030303;
    --bold-text-color: #4e4e4e;
    --border-color: #030303;
    --input-bg-color: #fff;
    --footer-border-color: #0008;
    --footer-color: #0072f5;
  }
}
</style>
