<template>
  <div class="login container mt-5">
    <!-- Barra de Navegação -->
    <nav class="mb-4">
      <button @click="voltarParaHome" class="btn btn-secondary">Voltar para Home</button>
    </nav>

    <h1 class="text-center">
      Faça seu Login
      <img class="logo-inline ms-2" src="@/assets/imagens/Fake.png" alt="Fake" />
    </h1>

    <form @submit.prevent="fazerLogin" class="mt-4">
      <div class="mb-3">
        <label for="username" class="form-label">Usuário</label>
        <input type="text" id="username" v-model="username" class="form-control" required />
      </div>
      <div class="mb-3">
        <label for="senha" class="form-label">Senha</label>
        <input type="password" id="senha" v-model="senha" class="form-control" required />
      </div>
      <button type="submit" class="btn btn-primary">Entrar</button>
      <p v-if="erro" class="text-danger mt-3">{{ erro }}</p>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      username: "",
      senha: "",
      erro: null,
    };
  },
  methods: {
    async fazerLogin() {
      try {
        const { data } = await axios.post("https://fakestoreapi.com/auth/login", {
          username: this.username,
          password: this.senha,
        });
        if (data.token) {
          localStorage.setItem("token", data.token);
          this.$router.push("/dashboard");
        }
      } catch {
        this.erro = "Usuário ou senha inválidos.";
      }
    },
    voltarParaHome() {
      this.$router.push("/");
    },
  },
};
</script>

<style>
/* Estilo geral do login */
body {
  font-family: 'Arial', sans-serif;
  background-color: #f4f7fb; /* Fundo claro com tonalidade de azul */
  color: #333; /* Cor de texto padrão */
  margin: 0;
  padding: 0;
}

/* Container do login */
.login {
  max-width: 400px;
  margin: 80px auto; /* Centraliza o conteúdo vertical e horizontalmente */
  padding: 30px;
  background-color: #fff; /* Fundo branco */
  border-radius: 12px;
  box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.1); /* Sombra leve */
}

/* Título do painel */
h1 {
  color: #002B5C; /* Azul escuro */
  font-size: 1.8rem;
  font-weight: bold;
  text-align: center;
  margin-bottom: 30px;
}

h1 .logo-inline {
  width: 40px;
  vertical-align: middle;
}

/* Barra de Navegação */
nav {
  display: flex;
  justify-content: flex-start;
}

nav .btn {
  background-color: #007BFF; /* Azul claro */
  color: #fff;
  border: none;
  padding: 10px 20px;
  font-weight: bold;
  border-radius: 5px;
  text-decoration: none;
  transition: background-color 0.3s ease;
}

nav .btn:hover {
  background-color: #0056b3; /* Azul escuro no hover */
}

/* Estilo dos campos de input */
.form-label {
  color: #002B5C; /* Azul escuro */
  font-size: 1rem;
}

.form-control {
  background-color: #f9f9f9; /* Fundo claro */
  border: 1px solid #007BFF; /* Bordas azuis */
  border-radius: 5px;
  padding: 10px;
  font-size: 1rem;
  color: #333;
  transition: border 0.3s ease;
}

.form-control:focus {
  border-color: #0056b3; /* Azul escuro quando em foco */
  box-shadow: 0px 0px 5px rgba(0, 43, 92, 0.3); /* Sombra suave no foco */
}

/* Botão de login */
.btn-primary {
  background-color: #007BFF;
  border: none;
  color: #fff;
  width: 100%;
  padding: 10px;
  font-weight: bold;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.btn-primary:hover {
  background-color: #0056b3; /* Azul escuro no hover */
}

/* Mensagem de erro */
.text-danger {
  color: #e74c3c; /* Vermelho para erro */
  text-align: center;
}

/* Responsividade */
@media (max-width: 768px) {
  .login {
    padding: 20px;
    margin: 60px auto;
  }

  h1 {
    font-size: 1.5rem;
  }
}

</style>