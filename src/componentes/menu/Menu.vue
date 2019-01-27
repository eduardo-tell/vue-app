<template>
    <div class="side">
        <img :src="dadosDoUsuario.avatar_url" alt="Imagem do usuario">
        <div class="text-left">
          <a class="nome-do-usuario" :href="dadosDoUsuario.html_url">{{dadosDoUsuario.name}}</a>
          <br>
          {{dadosDoUsuario.bio}} 
          <br>
        </div>
        <div class="anotacoes">
          <label for="Anotacoes">Anotacoes</label>
          <input type="text" class="anotacao" v-model="dadosDoUsuario.anotacoesDoUsuario" />
          <button id="anotacao" @click="salvarAnotacao">Salvar</button>
        </div>
    </div>
</template>

<script>
export default {

    props: ['dadosDoUsuario'],

    data() {
        return {
            anotacoesDoUsuario: ''
        }
    },

    methods: {        

        salvarAnotacao(){
            window.localStorage.setItem(this.dadosDoUsuario.login, this.anotacoesDoUsuario);      
        }
    }
}
</script>

<style scope>

.side{
    float: left;
    position: absolute;
    top: 65px;
    bottom: 0;
    left: 0;
    z-index: 2;
    width: 260px;
    background: #ececec;
    text-align: center;
    padding: 2% 2%;
}

.side img{
    border-radius: 90px;
    border: 2px solid #9c27b0;
    width: 100px;
}

.nome-do-usuario{
    font-size: 2em;
    margin: 6% auto;
    display: block;
    text-align: center;
    text-decoration: none;
}

.anotacoes{
    text-align: left;
    margin-top: 50px;
}

.anotacoes input{
    margin: 5% 0;
}

.anotacoes button{
    margin: 0;
    width: 100%;
    font-size: 16px;
    padding: 10px;
}
    
</style>