<template>
  <div class="main-container">
  <h1>Home - Cadastro do Produto e Fabricantes</h1>
  </div>
  <ProdutoForm />
</template>

<script>
import ProdutoForm from "../components/ProdutoForm.vue";
export default {
  name: "Home",
  components: {
    ProdutoForm
  }
}

</script>
