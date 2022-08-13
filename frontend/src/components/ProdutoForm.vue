<template>
    <div>
        <!-- <p>Componente de Mensagem</p> -->
        <div class="formularios">
            <form id="produto-form" method="POST" v-on:submit="createProduct">
                <div class="input-container">
                    <label for="nome">Nome do Produto</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o nome do Produto">
                </div>
                <div class="input-container">
                    <label for="nome">Fabricante</label>
                    <select name="fabricante" id="fabricante" v-model="fabricante">
                        <option value="">Selecione o fabricante</option>
                         <option v-for="fabricante in fabricantesCadastrados" :key="fabricante.id">{{fabricante.nome}}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="nome">Categoria</label>
                    <select name="categoria" id="categoria" v-model="categoria">
                        <option value="">Selecione a categoria</option>
                         <option v-for="fabricante in fabricantesCadastrados" :key="fabricante.id">{{fabricante.nome}}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="preco">Preço</label>
                    <input type="text" id="preco" name="preco" v-model="preco" placeholder="Digite o nome do Produto" >
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar produto">
                </div>
            </form>
            <div>

            <form id="produto-form" method="POST" v-on:submit="createFabricante">
                <div class="input-container">
                    <label for="nome">Nome do Fabricante</label>
                    <input type="text" id="nome" name="name" v-model="nomeFabricante" placeholder="Digite o nome do Produto">
                </div>
                
                <div class="input-container">
                    <label for="preco">Categoria</label>
                      <input type="text" id="categoria1" name="categoy" v-model="categoria1" placeholder="Digite o nome da primeira Categoria" >
                      <input type="text" id="categoria2" name="category" v-model="categoria2" placeholder="Digite o nome da segunda Categoria" >
                      <input type="text" id="categoria3" name="category" v-model="categoria3" placeholder="Digite o nome da terceira Categoria">
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar fabricante">
                </div>

            </form>
        </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ProdutoForm",
    data() {
        return {
            nomeFabricante: null,
            categoria1: null,
            categoria2: null,
            categoria3: null,
            nome: null,
            fabricante: null,
            categoria: null,
            preco: null,
            msg: null,
            fabricantesCadastrados: null
        }
    },
    methods: {
        async getCaracteristicas() {
            const req = await fetch("http://localhost:3000/fabricantesCadastrados");
            const data = await req.json();
            console.log(data.fabricantesCadastrados);
            this.fabricantesCadastrados = data.fabricantesCadastrados;
        },
        async createProduct(e) {
            e.preventDefault();
            console.log('criou o produto')

            const data = {
                nome:this.nome,
                fabricante: this.fabricante,
                categoria: this.categoria,
                preco: this.preco
            }
            console.log(data);
            // console.log(data);
            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/produtos", {
                method: 'POST',
                headers: {"Content-Type":"application/json"},
                body: dataJson
            });

            const res = await req.json();
            console.log(this.nome);
            console.log(res);

            //limpa os dados
            this.nome = "";
            this.fabricante = "";
            this.categoria = "";
            this.preco = "";
        },
        async createFabricante(e) {
             e.preventDefault();
             console.log('criou o fabricante');
              const data = {
                nomeFabricante:this.nomeFabricante,
                categoria1: this.categoria1,
                categoria2: this.categoria2,
                categoria3: this.categoria3
              }
              console.log(data);
              const dataJson = JSON.stringify(data);
              const req = await fetch("http://localhost:3000/fabricantesCadastrados", {
                method: 'POST',
                headers: {"Content-Type":"application/json"},
                body: dataJson
              });
               const res = await req.json();
               console.log(this.nome);
               console.log(res);
               //limpa os dados do fabricante
                this.nomeFabricante = "";
                this.categoria1 = "";
                this.categoria2 = "";
                this.categoria3 = "";

        }

    },
    mounted(){
        this.getCaracteristicas();
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
}
label {
    font-weight: bold;
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
.formularios {
    display: grid;
    grid-template-columns: 1fr 1fr;
}


</style>
