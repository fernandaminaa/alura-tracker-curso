<template>
    <header>
       <h1>
           <img src="../assets/logoAT.png">
       </h1>
       <button class="button" @click="alterarTema">
          {{textoBotao}}
       </button>
    </header>
   </template>
   
   <script lang="ts">
   import { defineComponent } from 'vue';
   
   export default defineComponent({
       name: 'BarraLateral',
       //para o componente filho se comunicar com o componente pai é através de eventos (emits)
       emits: ['aoTemaAlterado'], //recebe um array de string com todos os eventos que serão emitidos
       data(){
        return{
          modoEscuroAtivo: false
        }
       },
       computed:{
        textoBotao() {
          if(this.modoEscuroAtivo){
            return 'Desativar modo escuro'
          }
          return 'Ativar modo escuro'
        }
       },
       methods: {
        alterarTema (){
          this.modoEscuroAtivo = !this.modoEscuroAtivo            //primeiro deve-se alterar o valor
            this.$emit('aoTemaAlterado', this.modoEscuroAtivo)    //depois emitir o evento
        }
       }
   })
   </script>
   
   <style scoped>
   header {
     padding: 1rem;
     background: #0d3b66;
     width: 100%;
     height: 100vh;
     text-align:center;
   }
   @media only screen and (max-width: 768px) {
     header {
       padding: 2.5rem;
       height: auto;
     }
   }
   </style>