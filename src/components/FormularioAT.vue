<template>
  <div class="box formulario">
    <div class="columns">
      <div
        class="column is-8"
        role="form"
        aria-label="Formulario para criação de nova tarefa"
      >
        <input
          type="text"
          class="input"
          placeholder="Qual tarefa deseja iniciar?"
          v-model="descricao"
        />
      </div>
      <div class="column">
        <TemporizadorAT @ao-temporizador-finalizado="finalizarTarefa" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import TemporizadorAT from "./TemporizadorAT.vue";

export default defineComponent({
  name: "FormularioAT",
  emits: ['aoSalvarTarefa'],
  components: {
    TemporizadorAT,
  },
  data(){
    return{
        descricao: ''
    }
  },
  methods: {
    finalizarTarefa(tempoDecorrido: number): void {
        this.$emit('aoSalvarTarefa', {
            duracaoEmSegundos: tempoDecorrido,
            descricao: this.descricao
        })
      this.descricao =''
    },
  },
});
</script>

<style>
.formulario{
  color: var(--texto-primario);
  background-color: var(--bg-primario);
}
</style>
