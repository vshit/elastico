<template>
    <ul class="flex px-6 py-4 space-x-2">
        <li
            @click="setActiveGenre(genre.name)"
            class="border rounded-md px-5 py-3 hover:bg-blue-300 hover:cursor-pointer hover:text-white transition-all"
            :class="{ 'bg-blue-300 text-white': activeGenre === genre.name }"
            v-for="genre in genres"
            :key="genre.name"
        >
            {{ genre.name }}
        </li>
    </ul>
</template>

<script>
export default {
    props: {
        setActiveGenre: {
            type: Function,
            required: true,
        },
        activeGenre: {
            type: String,
            required: true,
        },
    },
    data: () => ({
        genres: [],
    }),
    methods: {
        async getGenres() {
            const res = await fetch("http://localhost:3000/genres");
            const data = await res.json();

            if (data) {
                this.genres = data;
            }
        },
    },
    mounted() {
        this.getGenres();
    },
};
</script>
