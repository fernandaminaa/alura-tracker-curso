<template>
    <div class="box has-text-weight-bold" :style="estilos">
        <slot></slot>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'BoxAT',
    //data = estado do componente
    data () {
        return {
            estilos: {
                background: '#FAF0CA'
            }
        }
    }
})
</script>