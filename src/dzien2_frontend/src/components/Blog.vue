<template>
    <button @click="getEntries">
        refresh
    </button>
    <div>
        <p v-for="entry in wpisy">
            {{ entry }}
        </p>
    </div>
</template>

<script>
import { dzien2_backend } from 'declarations/dzien2_backend/index';
export default {
    data() {
        return {
            wpisy: [],
            nowyBlog: ""
        }
    },
    methods: {
        async getEntries() {
            this.wpisy = await dzien2_backend.odczytaj_wpisy();
        },
        async addEntry() {
            await dzien2_backend.dodaj_wpis(this.nowyBlog);
        }
    },
    async mounted() {
        await this.getEntries()
    }
}
</script>