<template>
    <div class="container mx-auto px-3 py-10">
        <div class="grid grid-cols-1">
            <div class="flex flex-col md:flex-row md:gap-x-4 justify-between bg-white rounded-md overflow-hidden shadow-md hover:shadow-xl transition-all duration-500 relative">
                <img
                    :src="'https://image.tmdb.org/t/p/w500' + movieInfo.poster_path"
                    class="w-full md:w-64 transition-all duration-500 cursor-pointer"
                    alt="test">

                <div class="flex flex-col">
                    <div class="p-3 flex flex-col gap-y-4">
                        <div class="flex justify-between">
                            <h3 class="text-lg md:text-xl font-bold">
                                {{ movieInfo.original_title }}
                            </h3>
                        </div>
                        <div class="flex items-center gap-x-3 text-gray-700">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                            </svg>
                            <span>{{ movieInfo.release_date }}</span>
                        </div>
                        <div class="text-basic text-gray-500 h-24 overflow-hidden">
                            <p>{{ movieInfo.overview }}</p>
                        </div>
                    </div>
                    <span class="p-3 flex gap-x-4 items-center text-gray-600 bg-gray-100 md:bg-white cursor-pointer">
                    <img src="https://img.icons8.com/color/48/000000/imdb.png" alt=""/>
                    <span class="flex items-center gap-x-2">
                        {{ movieInfo.vote_average }}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-yellow-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z" />
                        </svg>
                    </span>

                    <span class="flex items-center gap-x-2">
                        {{ movieInfo.vote_count }}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-yellow-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                        </svg>
                    </span>
                </span>
                </div>

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
    async asyncData({ $axios, params }) {
        const movieId = params.movieId;
        const movieInfo = await $axios.$get(`https://api.themoviedb.org/3/movie/${movieId}?api_key=bf319d377842d32fdaadacb03d139006`)
        return {
            params,
            movieInfo
        }
    },
    data() {
        return {
        }
    },
    mounted() {
    }
}
</script>

<style scoped>

</style>
