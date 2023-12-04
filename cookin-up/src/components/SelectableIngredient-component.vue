<script lang="ts">
import Tag from './Tag-component.vue';

export default {
  components: { Tag },
  props: {
    ingrediente: { type: String, required: true }
  },
  data() {
    return {
      selecionado: false
    }
  },
  methods: {
    aoClicar() {
      this.selecionado = !this.selecionado

      this.$emit('adicionarIngrediente', this.ingrediente)
    }
  },
  emits: ['adicionarIngrediente']
}
</script>

<template>
  <button
    @click="aoClicar()"
    :aria-pressed="selecionado"
  >
    <Tag
      :texto="ingrediente"
      :ativa="selecionado"
    />
  </button>
</template>