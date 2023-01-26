<template>
    <BoxAT>
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column">
                <CronometroAT :tempoEmSegundos="tarefa.duracaoEmSegundos"/>
            </div>
        </div>
    </BoxAT>
</template>

<script lang="ts">
import ITarefa from '@/interfacesAT/ITarefaAT';
import { defineComponent, PropType } from 'vue';
import CronometroAT from './CronometroAT.vue';
import BoxAT from './BoxAT.vue';

export default defineComponent({
    name: 'TarefaAT',
    components: {
    CronometroAT,
    BoxAT
},
    props: {
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true
        }
    }
})
</script>

<style scoped>
.box{
    background: #faf0ca;
}
</style>