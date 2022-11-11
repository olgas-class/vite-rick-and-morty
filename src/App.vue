<script>
import axios from "axios";
import AppHeader from './components/AppHeader.vue';
import CharactersList from './components/CharactersList.vue';
import AppLoader from "./components/AppLoader.vue";
import AppSearch from "./components/AppSearch.vue";
import { store } from "./store";

export default {
  components: {
    AppHeader,
    CharactersList,
    AppLoader,
    AppSearch
  },
  data() {
    return {
      store
    }
  },
  created() {
    this.getCharacters();
  },
  methods: {
    getCharacters() {
      // Prima di iniziare la chiamata, metto loading a true
      this.store.loading = true;
      let apiUrl = "https://rickandmortyapi.com/api/character";

      // ESEMPIO CONCATENAZIONE DELL'URL PER PARAMETRI
      // // Se c'è searchKey oppure searchStatus, aggiungo ?
      // if (this.store.searchKey || this.store.searchStatus) {
      //   apiUrl += "?";
      // }
      // // Se c'è searchKey, aggiungo parametro name
      // if (this.store.searchKey !== "") {
      //   apiUrl += `name=${this.store.searchKey}`;
      //   if (this.store.searchStatus) {
      //     apiUrl += "&";
      //   }
      // }
      // // Se c' searchStatus, Aggiungo parametro status
      // if (this.store.searchStatus !== "") {
      //   apiUrl += `&status=${this.store.searchStatus}`;
      // }

      // OGGETTO PARAMS
      const urlParams = {}
      if (this.store.searchKey) {
        urlParams.name = this.store.searchKey;
      }
      if (this.store.searchStatus) {
        urlParams.status = this.store.searchStatus;
      }

      // Sibtassi ES6
      // const urlParams = {
      //   ...this.store.searchKey && { name: this.store.searchKey },
      //   ...this.store.searchStatus && { status: this.store.searchStatus }
      // }

      axios.get(apiUrl, {
        params: urlParams
      })
        .then((resp) => {
          // Qui gestiamo la risposta se tutto è andato bene
          this.store.characters = resp.data.results
        })
        .catch(error => {
          // Qui gestiamo l'errore
          this.store.characters = [];
        })
        .finally(() => {
          // Qui resetto loading a false perché i dati sono arrivati
          this.store.loading = false;
        })
    }
  }
}
</script>

<template>
  <AppHeader />
  <main>
    <div class="container">
      <!-- Faccio vedere la lista solo se la risposta è già arrivata dall'api -->
      <section class="my-4">
        <AppSearch @performSearch="getCharacters" />
      </section>
      <section>
        <AppLoader v-if="store.loading" />
        <CharactersList v-else />
      </section>
    </div>
  </main>
</template>

<style lang="scss">
@use "./styles/general.scss" as *;
</style>