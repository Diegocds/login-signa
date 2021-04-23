<template>
  <div class="home">
    <div class="home__header content ">
      <img src="@/assets/logo.svg" />
      <router-link to="/login" class="home__header__sair">Sair</router-link>
    </div>

    <h1 class="home__title content">Plataforma de alunos</h1>

    <table class="home__table content ">
      <thead>
        <tr>
          <th>Nome</th>
          <th>Email</th>
          <th>RA</th>
          <th>Turma</th>
          <th>Ações</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="aluno in alunos" :key="aluno.id">
          <td>{{ aluno.nome }}</td>
          <td>
            {{ aluno.email }}
          </td>
          <td>
            {{ aluno.ra }}
          </td>
          <td>
            {{ aluno.turma }}
          </td>
          <td>
            <a @click="modalEditar = true" hfre="#" >
              <img src="@/assets/editar-imagem.svg" />
            </a>
            <a @click="deletarAluno($event, aluno.id)" hfre="#">
              <img src="@/assets/lixeira.svg" />
            </a>
          </td>
        </tr>
      </tbody>
    </table>

    <div class="home__buttons content">
      <button class="home__buttons__voltar" >Voltar</button>
      <button @click="modal = true" class="home__buttons__adicionar">
        Novo aluno
      </button>
    </div>
    <Modal v-if="modal">
      <div class="modal">
        <div class="modal__header">
          <h3 class="modal__header__title">Cadastrar novo aluno</h3>
          <a @click="modal = false" href="#">
            <img src="@/assets/Vector.svg" alt="" />
          </a>
        </div>
        <form class="modal__form">
          <input
            type="text"
            placeholder="Nome"
            class="modal__form__input"
            v-model="nome"
          />
          <input
            type="email"
            placeholder="E-mail"
            class="modal__form__input"
            v-model="email"
          />
          <input
            type="text"
            placeholder="RA"
            class="modal__form__input"
            v-model="ra"
          />
          <input
            type="text"
            placeholder="Turma"
            class="modal__form__input"
            v-model="turma"
          />
          <button @click="addAluno" class="modal__form__btn">Adicionar</button>
        </form>
      </div>
    </Modal>

    <Modal v-if="modalEditar">
      <div class="modal">
        <div class="modal__header">
          <h3 class="modal__header__title">Cadastrar novo livro</h3>
          <a href="#" @click="modalEditar = false">
            <img src="@/assets/Vector.svg" />
          </a>
        </div>
        <form @submit="editarAluno" class="modal__form">
          <input
            type="text"
            placeholder="Nome do aluno"
            v-model="editar.nome"
            class="modal__form__input"
          />
          <input
            type="text"
            placeholder="E-mail do aluno"
            v-model="editar.email"
            class="modal__form__input"
          />
          <input
            type="text"
            placeholder="RA do aluno"
            v-model="editar.ra"
            class="modal__form__input"
          />
          <input
            type="text"
            placeholder="Turma do aluno"
            v-model="editar.turma"
            class="modal__form__input"
          />

          <button class="modal__form__btn-voltar">Voltar</button>
          <button class="modal__form__btn">Editar</button>
        </form>
      </div>
    </Modal>
  </div>
</template>

<script>
import axios from "axios";
import Modal from "@/components/Modal";
export default {
  data() {
    return {
      nome: "",
      email: "",
      ra: "",
      turma: "",
      modal: false,
      modalEditar: false,
      alunos: [],
       editar: {
        id: "",
        nome: "",
        email: "",
        ra: "",
        turma: "",
      },
    };
  },
  components: {
    Modal,
  },
  mounted() {
    this.carregarAlunos();
  },
  methods: {
    async addAluno(e) {
      e.preventDefault();
      if (
        this.nome === "" ||
        this.email === "" ||
        this.ra === "" ||
        this.turma === ""
      ) {
        alert("Preencha todos os campos");
      } else {
        const { data } = await axios.post("http://localhost:3000/alunos", {
          nome: this.nome,
          email: this.email,
          ra: this.ra,
          turma: this.turma,
        });
      this.modal = false
      }
      this.carregarAlunos();
      this.nome = "";
      this.email = "";
      this.ra = "";
      this.turma = "";
    },
    async carregarAlunos() {
      const { data } = await axios.get("http://localhost:3000/alunos");
      this.alunos = data;
    },
  async deletarAluno(e, id) {
      e.preventDefault();

      const { data } = await axios.delete(
        `http://localhost:3000/alunos/${id}`
      );

      this.carregarAlunos();
    },
    async editarAluno(e) {
      e.preventDefault();
      const { data } = await axios.put(
        `http://localhost:3000/biblioteca/${this.editar.id}`,
        {
          nome: this.editar.nome,
          email: this.editar.email,
          ra: this.editar.ra,
          turma: this.editar.turma,
        }
      );
      this.carregarAlunos();
    },
  },
};
</script>

<style lang="scss" scoped>
.content {
  margin: 0 auto;
  width: 70%;
}

.home {
  display: flex;
  flex-direction: column;
  background: #212121;
  width: 100%;
  height: 100%;
  &__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 30px 0;
    &__sair {
      color: #fff;
      text-decoration: none;
      cursor: pointer;
    }
  }
  &__title {
    color: #fff;
    margin: 10px auto 40px;
  }
  &__table {
    background: #303030;
    border-radius: 5px;
    border-collapse: collapse;
    thead {
      tr {
        th {
          padding: 10px 0;
          color: #fff;
          border-bottom: 1px solid #d0d0d6;
        }
      }
    }
    tbody {
      tr {
        td {
          padding: 10px 0;
          color: #626262;
          text-align: center;
          a {
            margin: 0 10px;
            cursor: pointer;
          }
        }
      }
    }
  }
  &__buttons {
    display: flex;
    justify-content: flex-end;
    margin-top: 20px;
    &__voltar {
      border: 1px solid #fff;
      border-radius: 5px;
      outline: 0;
      background: transparent;
      color: #fff;
      padding: 10px;
      width: 182px;
      margin-right: 10px;
      transition: 800ms;
      cursor: pointer;
      outline: 0;
      &:hover {
        background: #096e64;
        color: #fff;
      }
    }
    &__adicionar {
      border: 0;
      background: #02c9b5;
      border-radius: 5px;
      color: #fff;
      width: 182px;
      transition: 800ms;
      cursor: pointer;
      outline: 0;
      &:hover {
        background: #096e64;
      }
    }
  }
  .modal {
    display: flex;
    flex-direction: column;
    padding: 15px;
    width: 100%;
    &__header {
      display: flex;
      justify-content: space-between;
      padding: 10px;
      &__title {
        color: #02c9b5;
      }
    }
    &__form {
      display: flex;
      flex-wrap: wrap;
      padding: 10px;
      &__input {
        outline: 0;
        padding: 10px;
        width: calc(50% - 5px);
        margin-bottom: 10px;
        border-radius: 5px;
        border: 0;
        &:nth-child(1) {
          margin-right: 5px;
        }
        &:nth-child(3) {
          margin-right: 5px;
        }
      }
      &__btn {
        width: 116px;
        padding: 10px;
        border: 0;
        border-radius: 5px;
        background: #02c9b5;
        font-weight: 500;
        color: #fff;
        cursor: pointer;
        outline: 0;
        transition: 800ms;
        &:hover {
          background: #096e64;
        }
      }
      &__btn-voltar {
      border: 1px solid #fff;
      border-radius: 5px;
      outline: 0;
      background: transparent;
      color: #fff;
      padding: 10px;
      width: 116px;
      margin-right: 10px;
      transition: 800ms;
      cursor: pointer;
      &:hover {
        background: #096e64;
        color: #fff;
      }
    }
    }
  }
}
</style>
