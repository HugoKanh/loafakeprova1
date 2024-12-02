<template>
  <div class="container mt-4">
    <nav class="mb-4">
      <button class="btn btn-secondary" @click="voltarParaDashboard">Voltar ao Dashboard</button>
    </nav>

    <h2 class="text-primary mb-4">Lista de Usuários</h2>
    <button class="btn btn-success mb-3" @click="adicionarUsuario">Adicionar Usuário</button>
    <table class="table table-bordered table-striped">
      <thead class="table-dark">
        <tr>
          <th>ID</th>
          <th>Nome</th>
          <th>Email</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="usuario in usuarios" :key="usuario.id">
          <td>{{ usuario.id }}</td>
          <td>{{ usuario.name.firstname }} {{ usuario.name.lastname }}</td>
          <td>{{ usuario.email }}</td>
          <td>
            <button class="btn btn-info btn-sm me-2" @click="verDetalhes(usuario.id)">Ver Detalhes</button>
            <button class="btn btn-warning btn-sm" @click="editarUsuario(usuario.id)">Editar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>


<script>
import { mapState } from 'vuex';

export default {
  computed: {
    ...mapState(['usuarios']),
  },
  methods: {
    verDetalhes(id) {
      this.$router.push(`/dashboard/usuarios/${id}`);
    },
    adicionarUsuario() {
      this.$router.push('/dashboard/usuarios/novo');
    },
    editarUsuario(id) {
      this.$router.push(`/dashboard/usuarios/${id}/editar`);
    },
    voltarParaDashboard() {
      this.$router.push('/dashboard');
    },
  },
  created() {
    if (!this.usuarios.length) {
      this.$store.dispatch('fetchUsuarios');
    }
  },
};
</script>


<style scoped>
/* Estilo geral do contêiner */
.container {
  background-color: #f8f9fa;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

/* Estilo do botão de voltar */
.btn-secondary {
  background-color: #007bff;
  border-color: #0056b3;
  color: white;
  font-weight: bold;
}

.btn-secondary:hover {
  background-color: #0056b3;
  border-color: #004085;
}

/* Estilo dos títulos */
.text-primary {
  color: #007bff;
  font-size: 1.75rem;
  font-weight: 600;
}

/* Estilo do botão 'Adicionar Usuário' */
.btn-success {
  background-color: #28a745;
  border-color: #218838;
  color: white;
}

.btn-success:hover {
  background-color: #218838;
  border-color: #1e7e34;
}

/* Estilo da tabela */
.table {
  width: 100%;
  margin-bottom: 1rem;
  background-color: white;
  border-radius: 8px;
  overflow: hidden;
}

.table-bordered {
  border: 1px solid #dee2e6;
}

.table-dark {
  background-color: #343a40;
  color: white;
}

.table th, .table td {
  padding: 1rem;
  text-align: center;
}

.table th {
  font-weight: bold;
}

.table-striped tbody tr:nth-child(odd) {
  background-color: #f2f2f2;
}

/* Estilo dos botões dentro da tabela */
.btn-info {
  background-color: #17a2b8;
  border-color: #117a8b;
}

.btn-info:hover {
  background-color: #117a8b;
  border-color: #0c6e7a;
}

.btn-warning {
  background-color: #ffc107;
  border-color: #e0a800;
}

.btn-warning:hover {
  background-color: #e0a800;
  border-color: #d39e00;
}

.btn-sm {
  font-size: 0.875rem;
}

/* Estilo de hover na linha da tabela */
tbody tr:hover {
  background-color: #e9ecef;
}
</style>
