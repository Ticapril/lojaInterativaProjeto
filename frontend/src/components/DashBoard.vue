<template>
  <div id="produto-table">
    <div>
      <div id="produto-table-heading">
        <div class="order-id">#</div>
        <div>Produto</div>
        <div>Fabricante</div>
        <div>Categoria</div>
        <div>Preço</div>
        <div>Ações</div>
      </div>
    </div>

    <div id="produto-table-rows">
      <div class="produto-table-row" v-for="produto in produtos" :key="produto.id">
        <div class="order-number">{{ produto.id }}</div>
        <div>{{produto.nome}}</div>
        <div>{{produto.fabricante}}</div>
        <div>{{produto.categoria}}</div>
        <div>{{produto.preco}}</div>
        <div>
          <button class="delete-btn" @click="deleteProduto(produto.id)">Deletar</button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>


export default {
  name: "Dashboard",
  data() {
    return {
      produtos: null,
      produto_id: null,
      status: []
    }
  },
  methods: {
    async getProdutos(){
      const req = await fetch("http://localhost:3000/produtos");
      const data = await req.json();
      
      this.produtos = data;

      //resgatar status
    },
    async deleteProduto(id) {
      const req = await fetch(`http://localhost:3000/produtos/${id}`,{
        method: "DELETE",
      });

    const res = await req.json();
      console.log(id);
    
    this.getProdutos();
    }
  },
  mounted(){
    this.getProdutos();
  }
}
</script>

<style scoped>
#produto-table {
  max-width: 1200px;
  margin: 0 auto;
}

#produto-table-heading,
#produto-table-rows,
.produto-table-row {
  display: flex;
  flex-wrap: wrap;
}

#produto-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #000;
}

#produto-table-heading div, .burger-table-row div {
  width: 19%;

}

.produto-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #ccc;
}

#produto-table-heading .order-id,
.produto-table-row .order-number {
  width: 5%;
}

.delete-btn {
  background-color: #222;
  color: blue;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  
}

</style>
