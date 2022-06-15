<template>
  <div id="app">

    <nav>
      <div class="nav-wrapper">
        <a href="#" class="brand-logo center">Cadastro de clientes</a>
      </div>
    </nav>

    <div class="container">
      <form @submit.prevent="salvar">

        <label>DOCUMENTO</label>
        <input type="text" v-model="cliente.documento">
        <label>NOME</label>
        <input type="text" v-model="cliente.nome">

        <button class="waves-effect">Salvar<i class="material-icons left">save</i></button>

      </form>

      <table>

        <thead>

          <tr>
            <th>DOCUMENTO</th>
            <th>NOME</th>
          </tr>

        </thead>

        <tbody>

          <tr v-for="cliente of clientes" :key="cliente.id">

            <td>{{cliente.documento}}</td>
            <td>{{cliente.nome}}</td>
            <td>
              <button @click="deletar(cliente)" class="waves-effect btn-small red darken-1"><i>Excluir</i></button>
            </td>

          </tr>

        </tbody>

      </table>

    </div>

  </div>
</template>

<script>

import Cliente from './services/clientes'

export default {
  data() {
    return {
      cliente: {
        documento: '',
        nome: '',
      },
      clientes: []
    }
  },

  mounted(){
    Cliente.listar().then(response => {
      this.clientes = response.data;
    })
  },

  methods:{

    salvar(){
      Cliente.salvar(this.cliente).then(response =>{
        console.log(response.data)
        alert('Cliente cadastrado com sucesso!')
      })

    },

    deletar(cliente){
      Cliente.deletar(cliente).then(response => {
        this.listar()
        var error = response.data.errors
        console.log(error)
      })
    }

  }

}

</script>

<style>
</style>
