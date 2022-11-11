<script>
import { store } from "../store";
export default {
    name: "ResultMessage",
    data() {
        return {
            store
        }
    },
    computed: {
        charactersNumber() {
            return this.store.characters.length;
        }
    }
}
</script>

<template>
    <div class="text-center">
        <h5 v-if="charactersNumber === 0">Non ci sono risultati per la tua ricerca</h5>
        <h5 v-else>
            Abbiamo trovato {{ charactersNumber }}
            {{ charactersNumber === 1 ? 'personaggio' : 'personaggi' }}
        </h5>
    </div>
</template>