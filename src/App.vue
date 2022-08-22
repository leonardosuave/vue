<template>
  <div id="app">

    <h3>Cadastro: </h3>
    <small id="deuErro" v-show="deuErro"> Nome inválido!</small><br>
    <input type="text" placeholder="nome" v-model="nomeField"> <br>
    <input type="text" placeholder="email" v-model="emailField"> <br>
    <input type="number" placeholder="idade" v-model="idadeField"> <br>
    <button @click="cadastrar()"> Cadastrar </button>
    <hr>

    <h1>Guia Clientes</h1>
    <!--Uso de props :cliente ; condicional V-if :showIdade-->
    <Cliente :cliente="clienteLeonardo" :showIdade="true"/>
    <Cliente :cliente="clienteLeonardo" :showIdade="false"/>
    <Cliente :cliente="clienteLeonardo" :showTel="true"/>

    <!--Uso de props com array de objetos para condicional V-for-->
    <div v-for="(cliente,index) in clientes /*orderClientes -> adiciona a listagem do array clientes na ordem alfabética*/" :key="cliente.id">
      <h4>{{ index + 1}}</h4> <!--Refere-se a ordem do cliente no array-->
      <Cliente :cliente="cliente" @meDelete="deletarUsuario($event)"/>
    </div>

    <!--Prop sem objeto
      <Cliente nome="Leonardo Suave" email="leonardo.suave15@hotmail.com" idade="26"/>
    <Cliente nome="Tassiane Pinheiro" email="tassi_pinhei@hotmail.com" idade="29"/>
    <Cliente nome="Juditinha" email="judite@gmail.com" idade="2"/>
    -->
  </div>
</template>

<script>

//Import biblioteca Lodash
import _ from 'lodash'

import Cliente from './components/Cliente.vue';
export default {
  name: 'App',
  data(){
    return {
      deuErro: false,

      nomeField: "",
      emailField: "",
      idadeField: "",

      nomeDoLeonardo: "Leonardo S",
      clienteLeonardo: {
        nome: "Leo Suave",
        email: "leo@outlook.com",
        tel: 992718554,
        idade: 26
      },

      //Para estrutura V-for
      clientes: [
        {
          id: 1,
          nome: "Panterinha Suave",
          email: "Pantera@outlook.com",
          tel: 1693934222,
          idade: 64
        },
        {
          id: 1,
          nome: "Clovis Suave",
          email: "clovis@outlook.com",
          tel: 1693934241,
          idade: 64
        },
        {
          id: 2,
          nome: "Lucia Helena",
          email: "lucia@outlook.com",
          tel: 1631431320,
          idade: 58
        },
        {
          id: 3,
          nome: "Tassiane Pinheiro",
          email: "tassi@outlook.com",
          tel: 1693593829,
          idade: 29
        }
      ]
    }
  },
  components: {
    Cliente
  },
  methods: {
    cadastrar() {

      if(!this.nomeField || this.nomeField == ' ' || this.nomeField.length < 3) {
        this.deuErro = true
        console.log('Nome inválido')
      } else {

      //Para adicionar um novo objeto de cliente no array clientes.
      this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now()});

      //Para Apagar os campos do forms após registrar.
      this.nomeField = "",
      this.emailField = "",
      this.idadeField = ""

      this.deuErro = false
      }

    },
    deletarUsuario($event) {
      console.log('Recebendo evento.')
      const id = $event.idDoCliente
      const novoArray = this.clientes.filter(cliente => cliente.id != id)
      this.clientes = novoArray
    }
  },
  computed: {
    orderClientes() {
      return _.orderBy(this.clientes, ['nome'], ['asc'])
    }
  }
}
</script>

<style>
/*Estilo para componentes do HTML digitado neste arquivo apenas*/

  h1 {
    text-align: center;
  }

  #deuErro {
    color: red;
  }
</style>
