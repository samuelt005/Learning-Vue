<script lang="ts">
import Banner from './components/Banner-component.vue'
import FooterComponent from './components/Footer-component.vue';
import Main from './components/Main-component.vue'

export default {
  components: { Banner, MainContent: Main, FooterComponent }
}
</script>

<template>
  <Banner />
  <MainContent />
  <FooterComponent />
</template>

<style scoped></style>
