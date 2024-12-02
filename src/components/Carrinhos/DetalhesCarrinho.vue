<template>
    <div class="container mt-4">
        <h2 class="mb-4">Detalhes do Pedido #{{ carrinho.id }}</h2>
        <p><strong>Data:</strong> {{ formatarData(carrinho.date) }}</p>
        <h3>Produtos:</h3>
        <ul class="list-group mb-3">
            <li 
                v-for="produto in carrinho.products" 
                :key="produto.productId" 
                class="list-group-item d-flex justify-content-between align-items-center"
            >
                Produto ID: {{ produto.productId }} 
                <span>Quantidade: {{ produto.quantity }}</span>
            </li>
        </ul>
        <h3>Valor total:</h3>
        <p class="fw-bold text-success">R$ {{ calcularTotal(carrinho.products).toFixed(2) }}</p>
        <button 
            @click="voltar" 
            class="btn btn-primary"
        >
            Voltar
        </button>
    </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
    data() {
        return {
            carrinho: null,
        };
    },
    computed: {
        ...mapState(['carrinhos']),
    },
    methods: {
        formatarData(data) {
            return new Date(data).toLocaleDateString('pt-BR');
        },
        calcularTotal(produtos) {
            return produtos.reduce((total, produto) => {
                console.log("Produto:", produto); // Log do produto
                const price = parseFloat(produto.price);
                const quantity = parseInt(produto.quantity, 10);

                // Validar valores de price e quantity
                if (isNaN(price) || isNaN(quantity)) {
                    console.error("Produto com dados inválidos:", produto);
                    return total;
                }

                // Log de valores calculados
                console.log(`Preço: ${price}, Quantidade: ${quantity}, Total Parcial: ${price * quantity}`);

                return total + price * quantity;
            }, 0);
        },
        voltar() {
            this.$router.push('/dashboard/carrinhos');
        },
    },
    created() {
        const id = Number(this.$route.params.id);
        this.carrinho = this.carrinhos.find((c) => c.id === id);

        if (!this.carrinho) {
            console.error("Carrinho não encontrado!");
        }
    },
};
</script>
