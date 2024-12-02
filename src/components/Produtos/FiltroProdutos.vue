<template>
    <div class="container mt-3">
      <h2>Filtros</h2>
      <div class="mb-3">
        <label for="categoria" class="form-label">Categoria:</label>
        <select id="categoria" v-model="categoriaSelecionada" @change="emitirFiltro" class="form-select">
          <option value="">Todas</option>
          <option v-for="categoria in categorias" :key="categoria" :value="categoria">{{ categoria }}</option>
        </select>
      </div>
      <div class="mb-3">
        <label for="ordenar" class="form-label">Ordenar por:</label>
        <select id="ordenar" v-model="criterioOrdenacao" @change="emitirOrdenacao" class="form-select">
          <option value="price-asc">Preço: Menor para Maior</option>
          <option value="price-desc">Preço: Maior para Menor</option>
          <option value="rating-asc">Classificação: Menor para Maior</option>
          <option value="rating-desc">Classificação: Maior para Menor</option>
        </select>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      categorias: {
        type: Array,
        required: true,
      },
    },
    data() {
      return {
        categoriaSelecionada: '',
        criterioOrdenacao: 'price-asc',
      };
    },
    methods: {
      emitirFiltro() {
        this.$emit('filtrar', this.categoriaSelecionada);
      },
      emitirOrdenacao() {
        this.$emit('ordenar', this.criterioOrdenacao);
      },
    },
  };
  </script>
  