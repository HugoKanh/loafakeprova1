<template>
  <div class="container mt-4">
    <h2 class="text-primary mb-4">{{ usuario.id ? 'Editar Usuário' : 'Adicionar Usuário' }}</h2>
    <form @submit.prevent="salvarUsuario">
      <div class="mb-3">
        <label for="nome" class="form-label">Nome</label>
        <input id="nome" type="text" class="form-control" v-model="usuario.name.firstname" required />
      </div>
      <div class="mb-3">
        <label for="sobrenome" class="form-label">Sobrenome</label>
        <input id="sobrenome" type="text" class="form-control" v-model="usuario.name.lastname" required />
      </div>
      <div class="mb-3">
        <label for="email" class="form-label">Email</label>
        <input id="email" type="email" class="form-control" v-model="usuario.email" required />
      </div>
      <div class="mb-3">
        <label for="cidade" class="form-label">Cidade</label>
        <input id="cidade" type="text" class="form-control" v-model="usuario.address.city" required />
      </div>
      <div class="mb-3">
        <label for="rua" class="form-label">Rua</label>
        <input id="rua" type="text" class="form-control" v-model="usuario.address.street" required />
      </div>
      <button type="submit" class="btn btn-primary">
        {{ usuario.id ? 'Salvar Alterações' : 'Adicionar Usuário' }}
      </button>
    </form>
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
      usuario: {
        id: null,
        name: { firstname: '', lastname: '' },
        email: '',
        address: { city: '', street: '' },
      },
    };
  },
  created() {
    if (this.$route.params.id) {
      const id = Number(this.$route.params.id);
      const usuarioExistente = this.$store.state.usuarios.find(
        (u) => u.id === id
      );
      if (usuarioExistente) {
        Object.assign(this.usuario, usuarioExistente);
      }
    }
  },
  methods: {
    async salvarUsuario() {
      if (!this.usuario.name.firstname || !this.usuario.email) {
        alert('Por favor, preencha os campos obrigatórios: Nome e E-mail.');
        return;
      }
      try {
        if (this.usuario.id) {
          await this.$store.dispatch('atualizarUsuario', this.usuario);
        } else {
          const novoUsuario = await this.$store.dispatch(
            'adicionarUsuario',
            this.usuario
          );
          this.usuario.id = novoUsuario.id;
        }
        alert('Usuário salvo com sucesso!');
        this.$router.push('/dashboard/usuarios');
      } catch (error) {
        console.error('Erro ao salvar usuário:', error);
        alert('Ocorreu um erro ao salvar o usuário.');
      }
    },
  },
};
</script>
