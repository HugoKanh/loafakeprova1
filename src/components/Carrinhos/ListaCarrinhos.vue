<template>
    <div class="container mt-4">
      <!-- Barra de Navegação -->
      <nav class="mb-4">
        <button @click="voltarParaDashboard" class="btn btn-secondary">
          Voltar ao Dashboard
        </button>
      </nav>
  
      <h2 class="mb-4">Lista de Pedidos</h2>
      <table class="table table-striped">
        <thead class="table-dark">
          <tr>
            <th>ID</th>
            <th>Data</th>
            <th>Valor Total</th>
            <th>Status</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="carrinho in carrinhos" :key="carrinho.id">
            <td>{{ carrinho.id }}</td>
            <td>{{ formatarData(carrinho.date) }}</td>
            <td>R$ {{ calcularTotal(carrinho.products).toFixed(2) }}</td>
            <td><span class="badge bg-success">Concluído</span></td>
            <td>
              <button @click="verDetalhes(carrinho.id)" class="btn btn-primary btn-sm">
                Ver Detalhes
              </button>
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
      ...mapState(['carrinhos']),
    },
    async created() {
      // Verificar se os produtos foram carregados, caso contrário, carregar
      if (!this.$store.state.produtos || !this.$store.state.produtos.length) {
        await this.$store.dispatch('fetchProdutos');
      }
  
      // Carregar os carrinhos
      if (!this.carrinhos || !this.carrinhos.length) {
        await this.$store.dispatch('fetchCarrinhos');
      }
    },
    methods: {
      formatarData(data) {
        return new Date(data).toLocaleDateString('pt-BR');
      },
      calcularTotal(produtos) {
        console.log("Produtos recebidos para cálculo:", produtos);
        return produtos.reduce((total, produto) => {
          const price = parseFloat(produto.price);
          const quantity = parseInt(produto.quantity, 10);
          if (isNaN(price) || isNaN(quantity)) {
            console.error("Dados inválidos:", produto);
            return total;
          }
          return total + price * quantity;
        }, 0);
      },
      verDetalhes(id) {
        this.$router.push(`/dashboard/carrinhos/${id}`);
      },
      voltarParaDashboard() {
        this.$router.push('/dashboard');
      },
    },
  };
  </script>
  