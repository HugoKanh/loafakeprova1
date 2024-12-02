<template>
  <div>
    <h2>{{ produto.title }}</h2>
    <img :src="produto.image" :alt="produto.title" width="150" />
    <p><strong>Preço:</strong> R$ {{ produto.price.toFixed(2) }}</p>
    <p><strong>Categoria:</strong> {{ produto.category }}</p>
    <p><strong>Descrição:</strong> {{ produto.description }}</p>
    <p><strong>Classificação:</strong> {{ produto.rating.rate }} ({{ produto.rating.count }} avaliações)</p>
    <button @click="fechar">Fechar</button>
  </div>
</template>

<script>
export default {
  props: {
    produto: {
      type: Object,
      required: true,
    },
    onClose: {
      type: Function,
      required: true,
    },
  },
  methods: {
    fechar() {
      this.onClose();
    },
  },
};
</script>
