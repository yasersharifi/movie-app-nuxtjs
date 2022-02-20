<template>
    <div class="container mx-auto my-6 px-3">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
            <div v-for="(item, index) in movies"
                 :key="index"
                 class="flex flex-col justify-between bg-white rounded-md overflow-hidden shadow-md hover:shadow-xl transition-all duration-500 relative">
                <div>
                    <img :src="'https://image.tmdb.org/t/p/w500' + item.backdrop_path"
                         class="transform hover:scale-110 transition-all duration-500 cursor-pointer"
                         alt="test">
                    <div class="p-3 flex flex-col gap-y-4">
                        <h3 class="text-lg md:text-2xl font-bold">{{ item.original_title }}</h3>
                        <div class="text-basic text-gray-500 h-24 overflow-hidden">
                            <p>{{ item.overview }}</p>
                        </div>
                    </div>
                </div>
                <span class="p-3">{{ item.vote_average }}</span>

                <!-- start heart icon-->
                <span class="h-8 w-8 bg-white hover:bg-red-300 text-gray-400 hover:text-red-500 absolute top-2 left-2 flex items-center justify-center rounded-full cursor-pointer transition-all duration-300">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
                        </svg>
                    </span>
                <!-- end heart icon-->
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "AllMovies",
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

<style scoped>

</style>
