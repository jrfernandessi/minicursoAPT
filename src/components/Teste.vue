<template>
  <div>
    <button @click="less()" :disabled="contador==0">-</button>
    <Contador :numero="contador"/>
    <button @click="more()">+</button>
    <ul>
        <li v-for="nome in nomes" :key="nome">
            {{nome}}
        </li>
    </ul>
  </div>
</template>

<script>
import Contador from './Contador'
export default {
    components:{
        Contador
    },
  data() {
    return {
      nome: "Junior",
      contador: 0,
      nomes:[
          "Junior",
          "Eduardo",
          "Edson",
          "Alan"
      ]
    };
  },
  methods: {
    more() {
      this.contador++;
    },
    less(){
        this.contador--
    }
  }
};
</script>

<style>
</style>