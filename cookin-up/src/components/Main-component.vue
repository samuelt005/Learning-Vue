<script lang="ts">
import MyList from './MyList-component.vue';
import SelectIngridients from './SelectIngridients-component.vue'
import ShowRecipes from './ShowRecipes-component.vue';

type Page = 'SelectIngridients' | 'ShowRecipes';

export default {
  data() {
    return {
      ingredientes: [] as string[],
      conteudo: 'SelectIngridients' as Page
    };
  },
  components: { SelectIngridients, MyList, ShowRecipes },
  methods: {
    adicionarIngrediente(ingrediente: string) {
      const indice = this.ingredientes.indexOf(ingrediente);

      if (indice !== -1) {
        this.ingredientes.splice(indice, 1);
      } else {
        this.ingredientes.push(ingrediente);
      }
    },

    navegar(pagina: Page) {
      this.conteudo = pagina;
    }
  }

}
</script>

<template>
  <main class="conteudo-principal">
    <MyList :ingredientes="ingredientes" />

    <KeepAlive include="SelectIngridients">
      <SelectIngridients
        v-if="conteudo === 'SelectIngridients'"
        @adicionar-ingrediente="adicionarIngrediente"
        @buscar-receitas="navegar('ShowRecipes')"
      />

      <ShowRecipes
        v-else-if="conteudo === 'ShowRecipes'"
        :ingredientes="ingredientes"
        @editar-receitas="navegar('SelectIngridients')"
      />
    </KeepAlive>
  </main>
</template>

<style scoped>
.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #fffaf3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

@media only screen and (max-width: 1300px) {
  .conteudo-principal {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .conteudo-principal {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}
</style>
