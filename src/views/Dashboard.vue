<template>
  <div class="dashboard container">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <ul class="navbar-nav">
        <li class="nav-item">
          <button class="btn btn-danger" @click="sair">Sair</button>
        </li>
      </ul>
    </nav>

    <h1 class="my-4">
      Painel de Controle - Fakeboard
      <img class="logo-inline" src="@/assets/imagens/Fake.png" alt="Fake" />
    </h1>

    <section class="indicadores" v-if="carregando">
      <p>Carregando dados...</p>
    </section>

    <section class="indicadores" v-else>
      <div class="row">
        <div class="col-md-3">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Total de Produtos</h5>
              <p class="card-text">{{ produtos.length }}</p>
              <button class="btn btn-primary" @click="irPara('produtos')">Ver Produtos</button>
            </div>
          </div>
        </div>

        <div class="col-md-3">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Quantidade de Categorias</h5>
              <p class="card-text">{{ categorias.length }}</p>
            </div>
          </div>
        </div>

        <div class="col-md-3">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Total de Pedidos</h5>
              <p class="card-text">{{ carrinhos.length }}</p>
              <button class="btn btn-primary" @click="irPara('carrinhos')">Ver Pedidos</button>
            </div>
          </div>
        </div>

        <div class="col-md-3">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Total de Usuários</h5>
              <p class="card-text">{{ usuarios.length }}</p>
              <button class="btn btn-primary" @click="irPara('usuarios')">Ver Usuários</button>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
  data() {
    return {
      carregando: true,
    };
  },
  computed: {
    ...mapState(['produtos', 'categorias', 'carrinhos', 'usuarios']),
  },
  methods: {
    irPara(tipo) {
      switch (tipo) {
        case 'produtos':
          this.$router.push('/dashboard/produtos');
          break;
        case 'carrinhos':
          this.$router.push('/dashboard/carrinhos');
          break;
        case 'usuarios':
          this.$router.push('/dashboard/usuarios');
          break;
        default:
          break;
      }
    },
    sair() {
      // Aqui você pode adicionar lógica para logout, como limpar os dados de sessão
      this.$router.push('/login');
    },
  },
  created() {
    // Carregando os dados ao inicializar
    if (this.produtos.length === 0) {
      this.$store.dispatch('fetchProdutos');
    }
    if (this.categorias.length === 0) {
      this.$store.dispatch('fetchCategorias');
    }
    if (this.carrinhos.length === 0) {
      this.$store.dispatch('fetchCarrinhos');
    }
    if (this.usuarios.length === 0) {
      this.$store.dispatch('fetchUsuarios');
    }
    this.carregando = false;
  },
};
</script>

<style scoped>
/* Estilo Geral */
body {
  background-color: #fff; /* Fundo branco */
  font-family: Arial, sans-serif;
  color: #333;
}

.dashboard {
  padding: 20px;
}

/* Navbar */
.navbar {
  background-color: #003366; /* Azul escuro */
  color: white;
  border-bottom: 3px solid #0055cc; /* Azul mais claro */
}

.navbar .navbar-nav .nav-item .btn-danger {
  background-color: #e60000; /* Vermelho para o botão de sair */
  border: none;
}

.navbar .navbar-nav .nav-item .btn-danger:hover {
  background-color: #cc0000; /* Efeito de hover */
}

/* Título */
h1 {
  font-size: 2.5rem;
  color: #003366; /* Azul escuro */
  font-weight: bold;
  display: flex;
  align-items: center;
}

h1 .logo-inline {
  width: 40px;
  margin-left: 10px;
}

/* Cards */
.card {
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  background-color: #f7f7f7; /* Fundo claro para os cards */
}

.card-body {
  padding: 20px;
  background-color: #fff;
}

.card-title {
  font-size: 1.2rem;
  font-weight: bold;
  color: #003366; /* Azul escuro */
}

.card-text {
  font-size: 1.1rem;
  color: #333;
}

.btn-primary {
  background-color: #0055cc; /* Azul claro */
  border: none;
  font-weight: bold;
}

.btn-primary:hover {
  background-color: #003366; /* Azul escuro no hover */
}

.btn-danger {
  background-color: #e60000;
  border: none;
}

.btn-danger:hover {
  background-color: #cc0000;
}

/* Indicadores */
.indicadores p {
  font-size: 1.5rem;
  color: #003366;
}

/* Responsividade */
@media (max-width: 768px) {
  .col-md-3 {
    margin-bottom: 20px;
  }
}

</style>
