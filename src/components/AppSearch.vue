<script>
import { store } from "../store";

export default {
    name: "AppSearch",
    data() {
        return {
            store,
            statusOptions: ["alive", "dead", "unknown"]
        }
    }
}
</script>

<template>
    <div class="d-flex justify-content-center">
        <input type="text" class="form-control" v-model="store.searchKey">
        <select class="form-select" aria-label="Default select example" v-model="store.searchStatus">
            <option selected value="">Select status</option>
            <option v-for="(option, index) in statusOptions" :value="option" :key="index">{{ option }}</option>
        </select>
        <button class="btn btn-primary" @click="$emit('performSearch')">Search</button>
    </div>
</template>

<style lang="scss" scoped>

</style>