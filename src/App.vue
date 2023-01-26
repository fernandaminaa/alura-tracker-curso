<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema"/>
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioAT @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <TarefaAT v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <BoxAT v-if="listaVazia">
          Você ainda não realizou nenhuma tarefa hoje!
        </BoxAT>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import BoxAT from './components/BoxAT.vue';
import FormularioAT from './components/FormularioAT.vue';
import TarefaAT from './components/TarefaAT.vue';
import ITarefaAT from './interfacesAT/ITarefaAT';

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    FormularioAT,
    TarefaAT,
    BoxAT
  },
  data() {
    return {
      tarefas: [] as ITarefaAT[],
      modoEscuroAtivo: false
    }
  },
  methods: {
    salvarTarefa(tarefa: ITarefaAT) {
      this.tarefas.push(tarefa)
    },
    trocarTema (modoEscuroAtivo: boolean){
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  },
  computed: {
    listaVazia(): boolean {
      return this.tarefas.length === 0
    }
  }
});
</script>

<style>
.lista {
  padding: 1.25rem;
}
main{
  --bg-primario: #fff;
  --texto-primario: #000;
}
main.modo-escuro{
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}
.conteudo{
  background-color: var(--bg-primario);
}
</style>
