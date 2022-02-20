<template>
    <div class="w-full h-full bg-gray-200">
        <TheHeader />

        <!-- movies -->
        <div class="container mx-auto my-6 px-3">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                <div v-for="(item, index) in movies"
                     :key="index"
                     class="flex flex-col bg-white rounded-md overflow-hidden shadow-md hover:shadow-xl transition-all duration-500">
                    <img :src="'https://image.tmdb.org/t/p/w500' + item.backdrop_path"
                         class="transform hover:scale-110 transition-all duration-500 cursor-pointer"
                         alt="test">
                    <div class="p-3 flex flex-col gap-y-4">
                        <h3 class="text-lg md:text-2xl font-bold">{{ item.original_title }}</h3>
                        <p class="text-basic text-gray-500">{{ item.overview }}</p>
                        <span>{{ item.vote_average }}</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import TheHeader from "~/components/Templates/TheHeader";

export default {
        name: 'IndexPage',
        components: {
            TheHeader
        },
        data() {
            return {
                movies: []
            }
        },
        mounted() {
            const self = this;
            this.getMovies()
                .then(res => {
                    res.results.forEach(movie => {
                        self.movies.push(movie);
                    })
                })
        },
        methods: {
            async getMovies() {
                return await this.$axios.$get('https://api.themoviedb.org/3/movie/now_playing?api_key=bf319d377842d32fdaadacb03d139006');
            }
        }
    }
</script>
