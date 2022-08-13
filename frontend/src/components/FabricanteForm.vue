<template>
    <div>
        <p>Componente de Mensagem</p>
        <div>
            <form action="" id="produto-form">
                <div class="input-container">
                    <label for="nome">Nome do Fabricante</label>
                    <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite o nome do Produto">
                </div>
                
                <div class="input-container">
                    <label for="preco">Categoria</label>
                      <input type="text" id="categoria1" name="categoy" v-model="categoria1" placeholder="Digite o nome da primeira Categoria" >
                      <input type="text" id="categoria2" name="category" v-model="categoria2" placeholder="Digite o nome da segunda Categoria" >
                      <input type="text" id="categoria3" name="category" v-model="categoria3" placeholder="Digite o nome da terceira Categoria">
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar produto">
                </div>

            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: "FabricanteForm",
    data() {
        return {
            nome: null,
            categoria1: null,
            categoria2: null,
            categoria3: null
        }
    },
    methods: {
        async getProdutos() {
            const requisicao = await fetch("http://localhost:3000/caracteristicas");
            const data = await requisicao.json();
            console.log(data);
            this.fabricantes = data.fabricantes;
            this.categorias = data.categorias
        }
    },
    mounted(){
        this.getProdutos();
    }
}
</script>

<style scoped>
#produto-form {
    max-width: 400px;
    margin: 0 auto;
}
.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 10px;
}
label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
}

input, select {
    padding: 5px 10px;
    width: 300px;
}
.submit-btn {
    background-color: blue;
    color: #fff;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    /* font-size: 10px; */
    /* margin: 0 auto; */
    cursor: pointer;
    transition: .5s;
}
.submit-btn:hover {
    background-color: transparent;
    color: blue
}


</style>
