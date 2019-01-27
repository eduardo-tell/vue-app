
<template>
  <div class="core">

    <section class="menu">
      <input type="text" v-model="nomeUsuario" placeholder="Pesquise aqui" />

      <button type="button" @click="buscaUsuario">
        Buscar
      </button>
    </section>

    <menu-usuario :dadosDoUsuario="dadosDoUsuario" v-show="visivel"></menu-usuario>

    <repositorios :repositorios="repositorios" v-show="visivel"></repositorios>

    <section v-show="!visivel" class="ops">
        <h1> Ola! Pesquise algum usuário do GitHub a cima! </h1>
    </section>

  </div>
</template>

<script>
import Menu from '../menu/Menu.vue';
import Repositorios from '../repositorios/Repositorios.vue';

export default {

  components: {
    'menu-usuario' : Menu,
    'repositorios' : Repositorios
  },

  data() {
    return {
      visivel: false,
      nomeUsuario: '',
      dadosDoUsuario: '',
      repositorios: ''
    }
  },

  methods: {
    buscaUsuario(){
        this.buscaDadosUsuario(this.nomeUsuario).then(dados => {
            if(dados.message != 'Not Found') {
                this.dadosDoUsuario = dados;
                this.recuperaAnotacoes(dados.name);
                this.visivel =  true;
            } else {
                this.visivel =  false;
            } 
        });
        this.buscaRepositorios(this.nomeUsuario).then(repos => {
            if(repos.length > 0) {
                this.repositorios = repos;
                this.visivel =  true;
            } else {
              this.visivel =  false;
            }
        });
    },

    buscaDadosUsuario(nomeUsuario){
        return fetch(`https://api.github.com/users/${nomeUsuario}`)
              .then(response => response.json());
    },

    buscaRepositorios(nomeUsuario){
        return fetch(`https://api.github.com/users/${nomeUsuario}/repos`)
        .then(response => response.json());
    },    

    recuperaAnotacoes(dadosDoUsuario){
      let v = window.localStorage.getItem(this.nomeUsuario);
      if(v.key == dadosDoUsuario.login && v.key != null){
        this.dadosDoUsuario.anotacoesDoUsuario = v;
      } else {
        this.dadosDoUsuario.anotacoesDoUsuario = v;
      }       
    }
  }
}

</script>

<style>
*{
  font-family: Arial;
  font-weight: 100;
  color: #797979;
}
.menu{
  background-color: #ececec;
  display: flex;
  height: 65px;
  justify-content: space-between;
}
.esconde{
  display: none;
}
section.ops h1 {
    color: #9c27b0;
    text-align: center;
    margin: 40vh 0;
}
</style>
