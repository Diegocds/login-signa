<template>
  <div class="container">
    <div class="container__cadastro">
      <img src="@/assets/logo.svg" class="container__cadastro__img" />

      <h1 class="container__cadastro__titulo">Novo cadastro</h1>

      <form class="container__cadastro__form" @submit.prevent="save">
        <input type="text" placeholder="Digite seu nome" v-model="nome" />
        <!-- {{ nome }} -->
        <input
          type="text"
          placeholder="Digite seu sobrenome"
          v-model="sobrenome"
        />
        <input type="email" placeholder="Digite seu email" v-model="email" />
        <input type="password" placeholder="Digite sua senha" v-model="senha" />
        <input
          type="password"
          placeholder="Confirme sua senha"
          v-model="confirmarSenha"
        />
        <button type="submit" class="container__cadastro__form__button">
          Cadastrar
        </button>
      </form>
      <router-link to="/login" class="container__cadastro__voltar"
        >Voltar</router-link
      >
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      nome: "",
      sobrenome: "",
      email: "",
      senha: "",
      confirmarSenha: "",
    };
  },
  methods: {
    async save() {
      if (this.senha === this.confirmarSenha) {
        const data = await axios.post("http://localhost:3000/usuarios", {
          nome: this.nome,
          sobrenome: this.sobrenome,
          email: this.email,
          senha: this.senha,
        });
        alert("usuario cadastrado");
        this.$router.push("/login");
      } else {
        alert("Senhas não são iguais");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 100%;
  background: #212121;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  &__cadastro {
    display: flex;
    flex-direction: column;
    width: 30%;
    &__img {
      width: 140px;
      margin-bottom: 20px;
    }
    &__titulo {
      color: #fff;
      margin-bottom: 20px;
    }
    &__form {
      display: flex;
      flex-direction: column;
      input {
        padding: 10px;
        margin-bottom: 10px;
        border-radius: 5px;
        outline: 0;
        border: 0;
      }
      &__button {
        outline: 0;
        border: 0;
        color: #ffffff;
        background: #02c9b5;
        padding: 10px;
        border-radius: 5px;
        font-size: 16px;
        cursor: pointer;
        transition: 800ms;
        &:hover {
          background: #096e64;
        }
      }
    }
    &__voltar {
      border: 1px solid #02c9b5;
      text-decoration: none;
      padding: 10px;
      border-radius: 5px;
      margin-top: 20px;
      text-align: center;
      font-size: 16px;
      color: #fff;
      transition: 800ms;
      outline: 0;
      &:hover {
        background: #096e64;
      }
    }
  }
}
</style>
