<template>
  <div class="box formulario">
    <div class="columns">
      <div
        class="column is-8"
        role="form"
        aria-label="Formulário para criação de uma nova tarefa"
      >
        <input
          type="text"
          class="input"
          placeholder="Qual tarefa você deseja iniciar?"
          v-model="descricaoTarefa"
        />
      </div>

      <div class="column">
        <Temporizador @aoTemporizadoFinalizado="finalizarTarefa"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Temporizador from './Temporizador.vue'
export default defineComponent({
  name: 'Formulario',
  components: {
    Temporizador
  },
  data(){
    return{
      descricaoTarefa: '',
    }
  },
  methods: {
    finalizarTarefa(tempoDecorrido: number): void{
      this.$emit('aoSalvarTarefa', {
        duracaoEmSegundos: tempoDecorrido,
        descricao: this.descricaoTarefa
      })
      this.descricaoTarefa = '';
    }
  },
  emits: ['aoSalvarTarefa']
})
</script>

<style>
.formulario{
  background-color: var(--bg-primario);
  color: var(--texto-primario);
}
</style>