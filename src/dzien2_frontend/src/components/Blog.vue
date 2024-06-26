<template>
    <h2 class="text-blue-600">Wpisy na bloga:</h2>
    <div class="w-100 flex flex-row-reverse">
        <button @click="getEntries" class="bg-blue-600 rounded-md text-white p-4">
            refresh
        </button>
    </div>
    <div class="grid mx-6 gap-4 my-4">
        <div v-for="entry in wpisy" class="grid drop-shadow-xl bg-stone-300 p-4">
            <p>
                {{ entry }}
            </p>
        </div>
    </div>
    <div class="flex justify-center flex-col">
        <input type="text" v-model="nowyBlog" class="border-2 border-blue-600">
        <button @click="addEntry" class="bg-blue-600 rounded-md text-white p-4">
            dodaj
        </button>
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