<template>
  <div id="app">

    <nav>
      <div class="nav-wrapper blue darken-1">
        <a href="#" class="brand-logo center">Form Usuarios</a>
      </div>
    </nav>

    <div class="container">
    
      <form @submit.prevent="salvar">
     
          <label>Nome</label>
          <input type="text" placeholder="Nome" v-model="usuario.nome">
          <label>Sobrenome</label>
          <input type="text" placeholder="Sobrenome" v-model="usuario.sobrenome">
          <label>Email</label>
          <input type="email" placeholder="email@email.com" v-model="usuario.email">

          <button class="waves-effect waves-light btn-small">Salvar<i class="material-icons left">save</i></button>

      </form >

      <table>

        <thead>

          <tr>
            <th>NOME</th>
            <th>SOBRENOME</th>
            <th>EMAIL</th>
            <th>OPÇÕES</th>
          </tr>

        </thead>

        <tbody>
          
          <tr v-for="usuario of usuarios" :key="usuario.id">
            
            <td>{{usuario.first_name}}</td>
            <td>{{usuario.last_name}}</td>
            <td>{{usuario.email}}</td>
            <td>
              <button @click="editar(usuario)" class="waves-effect btn-small blue darken-1"><i class="material-icons">create</i></button>
              <button class="waves-effect btn-small red darken-1"><i class="material-icons">delete_sweep</i></button>
            </td>

          </tr>

        </tbody>
      
      </table>

    </div>

  </div>
</template>

<script>

import Usuario from './services/usuarios'

export default{

  data(){
    return{
      usuario:{
        id:'',
        nome:'',
        sobrenome:'',
        email:''
      },
      usuarios: []
    }
  },

  //carrega a nossa API
  mounted(){//chaves???
    this.listar()  
  },
  
  methods:{

    listar(){
      Usuario.listar().then(resposta => {
        console.log(resposta)
        this.usuarios = resposta.data.data
    })
  },

    salvar(){

      if(!this.usuario.id){
        Usuario.salvar(this.usuario).then(resposta => {
          this.usuario = {}
          this.resposta = resposta
          alert("Salvo com sucesso!")
          this.listar()
      })} 
      
      else{
        Usuario.atualizar(this.usuario).then(resposta => {
          this.usuario = {}
          this.resposta = resposta
          alert("Atualizado com sucesso!")
          this.listar()
      })}

  },

  editar(usuario){
      this.usuario = usuario
    }
}

}

</script>

<style>

</style>
