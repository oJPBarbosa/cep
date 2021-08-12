<template>
  <div id="container">
    <input type="text" v-model="cep_value" placeholder="Digite seu CEP (e.g. 12345678)" maxlength="8" />
    <input type="button" v-on:click="consultar" value="Consultar CEP" />
    <div id="data-container">
      <p>Estado: {{ state_value }}</p>
      <p>Cidade: {{ city_value }}</p>
      <p>Bairro: {{ neighborhood_value }}</p>
      <p>Logradouro: {{ street_value }}</p>
    </div>
  </div>
</template>

<script>
import cep from "cep-promise";

export default {
  name: "Consultor",
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
    consultar() {
      if (this.cep_value.length < 8) return alert("Insira um CEP válido!");

      cep(this.cep_value).then((res) => {
        const json = JSON.parse(JSON.stringify(res));
        this.state_value = json["state"];
        this.city_value = json["city"];
        this.neighborhood_value = json["neighborhood"];
        this.street_value = json["street"];
      });
    }
  },
};
</script>

<style scoped>
#container {
  height: 100%;

  display: flex;
  flex-direction: column;
  align-items: center;

  text-align: left;
}

input {
  border: none;
  outline: none;
}

input[type=text] {
  height: 50px;
  width: 300px;

  color: #ffffff;
  background: #0e1224;

  border-bottom: 3px solid #ffffff;
  border-radius: 1px;

  font-size: 18px;
}

::placeholder {
  color: #ffffff;

  font-family: sf;
  font-size: 18px;
}

input[type=button] {
  height: 50px;
  width: 100%;

  color: #ffffff;
  background: #3485e4;

  cursor: pointer;

  font-family: sf;
  font-size: 18px;

  margin-top: 20px;
  
  transition: background 0.3s ease-in-out;
}

input[type=button]:hover {
  color: #e2e2e2;
  background: #2965af;

  transition: background 0.2s ease-in-out;
}

#data-container {
  width: 100%;
  height: 100%;

  font-size: 18px;
  
  text-align: left;

  margin-top: 20px;
}

p {
  margin-top: 5px;
}
</style>
