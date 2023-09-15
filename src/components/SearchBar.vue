<template>
    <div class="search-container">
        <input type="text" v-model="searchValue">
    </div>
    <p>{{searchValue}}</p>
</template>

<script>
import { ref } from 'vue'
export default {
    setup() {

        const searchValue = ref('')



        return {
            searchValue
        }
    }

}
</script>

<style>

</style>