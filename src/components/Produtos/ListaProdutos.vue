<template>
  <div class="container mt-5">
    <nav>
      <button @click="voltarParaDashboard" class="btn btn-link">Voltar ao Dashboard</button>
    </nav>

    <h1>Lista de Produtos</h1>

    <!-- Filtro de Produtos -->
    <FiltroProdutos
      :categorias="categorias"
      @filtrar="aplicarFiltro"
      @ordenar="aplicarOrdenacao"
    />

    <!-- Botão Adicionar Produto -->
    <button class="btn btn-primary mt-3" @click="abrirFormularioAdicionar">Adicionar Produto</button>

    <table class="table table-bordered mt-3">
      <thead>
        <tr>
          <th>Nome</th>
          <th>Categoria</th>
          <th>Preço</th>
          <th>Classificação</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="produto in produtosFiltrados" :key="produto.id">
          <td>{{ produto.title }}</td>
          <td>{{ produto.category }}</td>
          <td>R$ {{ produto.price.toFixed(2) }}</td>
          <td>{{ produto.rating.rate }} ({{ produto.rating.count }} avaliações)</td>
          <td>
            <button @click="abrirDetalhes(produto)" class="btn btn-info">Ver Detalhes</button>
            <button @click="editarProduto(produto)" class="btn btn-warning">Editar</button>
            <button @click="removerProduto(produto.id)" class="btn btn-danger">Excluir</button>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Modal de Detalhes -->
    <div v-if="produtoSelecionado" class="modal-overlay" @click.self="fecharDetalhes">
      <div class="modal-content">
        <DetalhesProdutos :produto="produtoSelecionado" :onClose="fecharDetalhes" />
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';
import FiltroProdutos from './FiltroProdutos.vue';
import DetalhesProdutos from './DetalhesProdutos.vue';

export default {
  components: { FiltroProdutos, DetalhesProdutos },
  data() {
    return {
      produtoSelecionado: null,
      categoriaSelecionada: '',
      criterioOrdenacao: 'price-asc',
      produtosFiltrados: [],
      categorias: [],
    };
  },
  computed: {
    ...mapState(['produtos']),
  },
  watch: {
    produtos: {
      immediate: true,
      handler() {
        this.produtosFiltrados = [...this.produtos];
        this.carregarCategorias();
      },
    },
  },
  methods: {
    aplicarFiltro(categoria) {
      this.categoriaSelecionada = categoria;
      this.aplicarFiltrosEOrdenacao();
    },
    aplicarOrdenacao(criterio) {
      this.criterioOrdenacao = criterio;
      this.aplicarFiltrosEOrdenacao();
    },
    aplicarFiltrosEOrdenacao() {
      let produtos = [...this.produtos];

      if (this.categoriaSelecionada) {
        produtos = produtos.filter((produto) => produto.category === this.categoriaSelecionada);
      }

      if (this.criterioOrdenacao === 'price-asc') {
        produtos.sort((a, b) => a.price - b.price);
      } else if (this.criterioOrdenacao === 'price-desc') {
        produtos.sort((a, b) => b.price - a.price);
      } else if (this.criterioOrdenacao === 'rating-asc') {
        produtos.sort((a, b) => a.rating.rate - b.rating.rate);
      } else if (this.criterioOrdenacao === 'rating-desc') {
        produtos.sort((a, b) => b.rating.rate - a.rating.rate);
      }

      this.produtosFiltrados = produtos;
    },
    carregarCategorias() {
      const categorias = [...new Set(this.produtos.map((produto) => produto.category))];
      this.categorias = categorias;
    },
    abrirDetalhes(produto) {
      this.produtoSelecionado = produto;
    },
    fecharDetalhes() {
      this.produtoSelecionado = null;
    },
    voltarParaDashboard() {
      this.$router.push('/dashboard');
    },
    abrirFormularioAdicionar() {
      this.$router.push('/dashboard/produtos/novo'); // Navega para página de adição
    },
    editarProduto(produto) {
      this.$router.push(`/dashboard/produtos/${produto.id}/editar`); // Navega para página de edição
    },
    async removerProduto(produtoId) {
      try {
        await this.$store.dispatch('removerProduto', produtoId);
        alert('Produto removido com sucesso!');
      } catch (error) {
        console.error('Erro ao remover produto:', error);
      }
    },
  },
  created() {
    if (this.produtos.length === 0) {
      this.$store.dispatch('fetchProdutos');
    }
  },
};
</script>
