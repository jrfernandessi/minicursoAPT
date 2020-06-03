<template>
  <div>
      <h1>Adicionar produto</h1>
      Nome: <input v-model="produto.nome"><br>
      Quantidade: <input v-model="produto.quantidade"><br>
      Preço: <input v-model="produto.preco"><br>
      <button @click="adicionarProduto()">Adicionar Produto</button><br>
      <hr>
    <h1>Lista de produtos</h1>
    <ul>
        <li v-for="produto in produtos" :key="produto.id">
            <span>{{produto.nome}} - R$ {{produto.preco}} - {{produto.quantidade}}</span>
            <button @click="adicionarNoCarrinho(produto)" :disabled="produto.quantidade==0">Adicionar ao Carrinho</button>
            <br>
            <div v-if="produto.quantidade<=2">
                <span :class="{alerta:produto.quantidade<=1}">estoque baixo</span><br>
                <input v-model="quantidadeCompra"/>
                <button @click="adicionarProdutoEstoque(produto)">Adicionar Produto ao Estoque</button>
            </div>
        </li>
    </ul>
    <hr>
    <h1>Carrinho</h1>
    <ul>
        <li v-for="produto in carrinho" :key="produto.id">
            <span>{{produto.nome}} - {{produto.quantidadeNoCarrinho}}</span>
        </li>
    </ul>
    <span>Valor Toral: R$ {{valorTotal}}</span>
  </div>
</template>

<script>
export default {
    data(){
        return {
            produto:{},
            valorTotal: 0,
            quantidadeCompra:0,
            produtos:[{
                nome: 'Skol',
                quantidade: 10,
                preco: 2.10
            }],
            carrinho:[]
        }
    },
    methods: {
        adicionarProduto(){
            this.produtos.push(this.produto)
            this.produto={}
        },
        adicionarNoCarrinho(produto){
            
            
            let flag = false
            for (const aux of this.carrinho) {
                if(aux.nome==produto.nome){
                    flag=true
                    aux.quantidadeNoCarrinho++
                    this.valorTotal+=parseFloat(produto.preco)
                }
            }
            if(!flag){
                produto.quantidadeNoCarrinho=1
                this.carrinho.push(produto)
                this.valorTotal+=parseFloat(produto.preco)
            }
            produto.quantidade--
        },
        adicionarProdutoEstoque(produto){
            produto.quantidade+=this.quantidadeCompra
            this.quantidadeCompra=0
        }
    }
}
</script>

<style>
    .alerta{
        color: red;
    }
</style>