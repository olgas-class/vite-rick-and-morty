<script>
import { store } from "../store";
import CharacterCard from "./CharacterCard.vue";
import ResultMessage from "./ResultMessage.vue";

export default {
    name: "CharactersList",
    components: {
        CharacterCard,
        ResultMessage
    },
    data() {
        return {
            store
        }
    }
}
</script>

<template>
    <ResultMessage />

    <h2 class="text-center">Lista personaggi</h2>

    <div class="row row-cols-2 row-cols-md-4 g-3">
        <div class="col" v-for="character in store.characters" :key="character.id">
            <CharacterCard :character="character" />
        </div>
    </div>
</template>

<style lang="scss" scoped>

</style>