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
        <tr>
          <td>Amanda</td>
          <td>
            amanda@angis.com.br
          </td>
          <td>
            190853
          </td>
          <td>
            ADS3A
          </td>
          <td>
            <a hfre="#">
              <img src="@/assets/editar.png" />
            </a>
            <a hfre="#">
              <img src="@/assets/delete.png" />
            </a>
          </td>
        </tr>
      </tbody>
    </table>

    <div class="home__buttons content">
      <button class="home__buttons__voltar">Voltar</button>
      <button class="home__buttons__adicionar">Novo aluno</button>
    </div>
  </div>
</template>

<script></script>

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
      &:hover {
        background: #fff;
        color: #000;
      }
    }
    &__adicionar {
      border: 0;
      background: #6202ee;
      border-radius: 5px;
      color: #fff;
      width: 182px;
      transition: 800ms;
      cursor: pointer;
      &:hover {
        background: rgb(69, 15, 150);
      }
    }
  }
}
</style>
