<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroAT :tempoEmSegundos="tempoEmSegundos" />
        <button class="button" @click="iniciar" :disabled="cronometroRodando">
            <span class="icon">
                <i class="fas fa-play"></i>
            </span>
            <span>play</span>
        </button>
        <button class="button" @click="finalizar" :disabled="!cronometroRodando">
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span>
            <span>stop</span>
        </button>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CronometroAT from './CronometroAT.vue';

export default defineComponent({
    name: "TemporizadorAT",
    emits: ['aoTemporizadorFinalizado'],
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        };
    },
    computed: {
        tempoDecorrido(): string {
            return new Date(this.tempoEmSegundos * 1000).toISOString().substr(11, 8);
        }
    },
    methods: {
        iniciar() {
            //começar a contagem
            //1 seg = 1000 ms
            //setInterval é do JS e não do vue 
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                //console.log('incrementando oo contador')
                this.tempoEmSegundos += 1;
            }, 1000);
                //no inspecionar na opção console.log consigo ver se cliquei na função de iniciar (play)
        },
        finalizar() {
            this.cronometroRodando = false
            clearInterval(this.cronometro);
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
            //no inspecionar na opção console consigo ver se cliquei na função de finalizar (stop) - console.log("finalizando");
        }
    },
    components: { 
        CronometroAT 
    }
})
</script>