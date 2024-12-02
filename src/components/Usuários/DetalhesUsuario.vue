<template>
    <div v-if="usuario" class="container mt-4">
      <h2 class="text-primary mb-4">Detalhes do Usuário</h2>
      <p><strong>Nome:</strong> {{ usuario.name.firstname }} {{ usuario.name.lastname }}</p>
      <p><strong>Email:</strong> {{ usuario.email }}</p>
      <p><strong>Cidade:</strong> {{ usuario.address.city }}</p>
      <p><strong>Rua:</strong> {{ usuario.address.street }}</p>
      <button class="btn btn-secondary mt-3" @click="voltar">Voltar</button>
    </div>
    <div v-else-if="carregando" class="text-center mt-4">
      <p class="text-info">Carregando usuário...</p>
    </div>
    <div v-else class="text-center mt-4">
      <p class="text-danger">Usuário não encontrado!</p>
    </div>
  </template>
  
  
  <script>
  import { mapState } from 'vuex';
  
  export default {
      computed: {
      ...mapState(['usuarios']),
    },
    data() {
      return {
        usuario: null,
        carregando: true,
      };
    },
    created() {
      const id = Number(this.$route.params.id);
      this.$store.dispatch('fetchUsuarios')
        .then(() => {
          this.usuario = this.$store.state.usuarios.find((u) => u.id === id);
        })
        .catch((error) => {
          console.error('Erro ao buscar usuários:', error);
        })
        .finally(() => {
          this.carregando = false;
        });
    },
    methods: {
      voltar() {
        this.$router.push('/dashboard/usuarios');
      },
    },
  };
  </script>
  