<template>
  <div id="consultor">
    <p id="header">
      Consulte seu CEP
      <img
        src="https://img.icons8.com/emoji/50/000000/globe-with-meridians-emoji.png"
      />
    </p>
    <input
      type="text"
      v-model="cep_value"
      placeholder="Digite seu CEP (e.g. 12345678)"
      maxlength="8"
    />
    <input
      type="button"
      id="consultar"
      v-on:click="consultar"
      value="Consultar CEP"
    />
    <div id="data-container">
      <p>Estado: {{ state_value }}</p>
      <p>Cidade: {{ city_value }}</p>
      <p>Bairro: {{ neighborhood_value }}</p>
      <p>Logradouro: {{ street_value }}</p>
    </div>
    <input type="button" id="limpar" v-on:click="limpar" value="Limpar" />
    <div id="footer">
      <p>
        Feito com 💙 por
        <a href="https://github.com/oJPBarbosa" target="_blank" rel="noreferrer"
          >oJPBarbosa</a
        >.
      </p>
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
      if (this.cep_value.length < 8)
        return alert("Insira um CEP válido no Brasil!");

      cep(this.cep_value).then((res) => {
        const json = JSON.parse(JSON.stringify(res));
        this.state_value = json["state"];
        this.city_value = json["city"];
        this.neighborhood_value = json["neighborhood"];
        this.street_value = json["street"];
      });
      
      document.getElementById("limpar").style.display = "block";
    },
    limpar() {
      this.cep_value = "";
      this.state_value = "";
      this.city_value = "";
      this.neighborhood_value = "";
      this.street_value = "";

      document.getElementById("limpar").style.display = "none";
    },
  },
};

</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300&display=swap");

#consultor {
  height: 100%;
  width: 20vw;
  min-width: 272px;

  display: flex;
  flex-direction: column;
  align-items: center;

  text-align: left;
}

#header {
  width: 100%;

  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;

  margin-bottom: 15px;

  font-size: 26px;
  font-weight: 600;
  font-family: "Poppins", sans-serif;
}

img {
  height: 38px;
  margin-left: 5px;
}

input {
  border: none;
  outline: none;
}

input[type="text"] {
  height: 50px;
  width: 100%;

  color: #ffffff;
  background: #0e1224;

  border-bottom: 3px solid #ffffff;
  border-radius: 1px;

  font-size: 18px;
  font-style: sf;
}

::placeholder {
  color: #ffffff;

  font-family: sf;
  font-size: 18px;
}

input[type="button"] {
  height: 50px;
  width: 100%;

  color: #ffffff;
  cursor: pointer;

  font-family: sf;
  font-size: 18px;

  margin-top: 20px;

  border-radius: 7.5px;

  transition: background 0.15s ease-in-out;
}

input[type="button"]:hover {
  color: #dad8d8;

  transition: background 0.1s ease-in-out;
}

#consultar {
  background: #3485e4;
}

#consultar:hover {
  background: #2965af;
}

#data-container {
  height: 100%;
  width: 100%;

  font-size: 18px;

  text-align: left;

  margin-top: 20px;
}

#data-container p {
  margin-top: 5px;
}

#limpar {
  display: none;

  margin-top: 25px;

  background: #db3030;
}

#limpar:hover {
  background: #a82020;
}

#footer {
  height: 100%;

  font-size: 18px;

  text-align: center;

  margin: 2.5vh;
}

#footer a {
  color: #55a2fa;

  text-decoration: none;

  border-bottom: 2px solid #fff8;

  transition: color 0.15s ease-out, border 0.15s ease-out;
}

#footer a:hover {
  color: #3683da;

  border-bottom-color: #3683da;

  transition: color 0.15s ease-in, border 0.15s ease-in;
}

@media screen and (max-width: 1350px) {
  #consultor {
    width: 30vw;
  }
}

@media screen and (max-width: 900px) {
  #consultor {
    width: 50vw;
  }
}

@media screen and (max-width: 550px) {
  #consultor {
    width: 75vw;
  }
}

@media screen and (max-width: 355px) {
  #consultor {
    width: 85vw;
  }
}
</style>
