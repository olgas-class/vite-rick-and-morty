<script>
import axios from "axios";
import AppHeader from './components/AppHeader.vue';
import CharactersList from './components/CharactersList.vue';
import AppLoader from "./components/AppLoader.vue";
import { store } from "./store";

export default {
  components: {
    AppHeader,
    CharactersList,
    AppLoader
  },
  data() {
    return {
      store
    }
  },
  created() {
    // Prima di iniziare la chiamata, metto loading a true
    this.store.loading = true;
    axios.get("https://rickandmortyapi.com/api/character").then((resp) => {
      this.store.characters = resp.data.results;
      console.log(this.store.characters);
      // Qui resetto loading a false perché i dati sono arrivati
      this.store.loading = false;
    });

  }
}
</script>

<template>
  <AppHeader />
  <main>
    <div class="container">
      <!-- Faccio vedere la lista solo se la risposta è già arrivata dall'api -->
      <AppLoader v-if="store.loading" />
      <CharactersList v-else />
    </div>
  </main>
</template>

<style lang="scss">
@use "./styles/general.scss" as *;
</style>