<template>
      <ul v-if="paginasTotal > 1">
        <li v-for="pagina in paginasTotal" :key="pagina">
          <router-link :to="{query: query(pagina)}"> {{ pagina }}</router-link>
        </li>
      </ul>
</template>

<script>
export default {
  name: "ProdutosPaginar",
  props: {
    produtosPorPagina: {
      type: Number,
      defalt: 1
    },
    produtosTotal: {
      type: Number,
      default: 1
    }
  },
  computed: {
    paginasTotal() {
      const total = Math.ceil(this.produtosTotal /  this.produtosPorPagina);
      return (total !== Infinity) ? Math.ceil(total) : 0;
    }
  },
  methods: {
    query(pagina) {
      return {
        ...this.$route.query,
        _page: pagina
      }
    }
  },
}
</script>

<style scoped>
  ul {
    grid-column: 1 / -1;
  }
  li {
    display: inline-block;
  }
  li a {
    padding: 2px 8px;
    border-radius: 2px;
    margin: 4px;
  }
  li a.router-link-exact-active {
    background: #87f;
    color: #fff;
  }
  li a:hover {
      background: #87f;
    color: #fff;
  }
</style>