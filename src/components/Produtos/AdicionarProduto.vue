<template>
  <div class="container mt-5">
    <h2>{{ produto.id ? "Editar Produto" : "Adicionar Produto" }}</h2>
    <form @submit.prevent="salvarProduto">
      <div class="mb-3">
        <label for="titulo" class="form-label">Título:</label>
        <input id="titulo" v-model="produto.title" class="form-control" required />
      </div>
      <div class="mb-3">
        <label for="imagem" class="form-label">Imagem (URL):</label>
        <input id="imagem" v-model="produto.image" class="form-control" required />
      </div>
      <div class="mb-3">
        <label for="preco" class="form-label">Preço:</label>
        <input id="preco" type="number" step="0.01" v-model="produto.price" class="form-control" required />
      </div>
      <div class="mb-3">
        <label for="categoria" class="form-label">Categoria:</label>
        <input id="categoria" v-model="produto.category" class="form-control" required />
      </div>
      <div class="mb-3">
        <label for="descricao" class="form-label">Descrição:</label>
        <textarea id="descricao" v-model="produto.description" class="form-control" required></textarea>
      </div>
      <button type="submit" class="btn btn-primary">
        {{ produto.id ? "Salvar Alterações" : "Adicionar" }}
      </button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      produto: {
        id: null,
        title: '',
        image: '',
        price: 0,
        category: '',
        description: '',
      },
    };
  },
  created() {
    const produtoId = this.$route.params.id;
    if (produtoId) {
      this.carregarProduto(produtoId);
    }
  },
  methods: {
    async carregarProduto(id) {
      try {
        const produto = this.$store.state.produtos.find(
          (p) => p.id.toString() === id.toString()
        );
        if (produto) {
          this.produto = { ...produto };
        } else {
          console.error("Produto não encontrado");
        }
      } catch (error) {
        console.error("Erro ao carregar produto:", error);
      }
    },
    async salvarProduto() {
      try {
        if (this.produto.id) {
          // Se o produto tiver um ID, está sendo editado
          await this.$store.dispatch("editarProduto", this.produto);
          alert("Produto editado com sucesso!");
        } else {
          // Caso contrário, é um novo produto
          await this.$store.dispatch("adicionarProduto", this.produto);
          alert("Produto adicionado com sucesso!");
        }
        this.$router.push("/dashboard/produtos");
      } catch (error) {
        console.error("Erro ao salvar produto:", error);
      }
    },
  },
};
</script>
