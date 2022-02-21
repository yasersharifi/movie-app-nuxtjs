<template>
    <div class="container mx-auto px-3 py-10">
        <!-- search -->
        <div class="mb-8">
            <div class="w-full md:w-96 relative bg-white flex items-center justify-between rounded overflow-hidden">
                <input v-model="searchText" @blur="searchMovies" type="text" class="w-full py-3 px-3 focus:border-0">
                <span class="flex items-center justify-center cursor-pointer">
                    <svg xmlns="http://www.w3.org/2000/svg" class="mx-3 h-6 w-6 text-gray-400 hover:text-gray-600 transition-all duration-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                    </svg>
<!--                    <svg v-show="searchText" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-400 hover:text-gray-600 cursor-pointer" fill="none" viewBox="0 0 24 24" stroke="currentColor">-->
<!--                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />-->
<!--                    </svg>-->
                </span>
            </div>
        </div>
        <!-- all movie -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
            <div
                v-for="(item, index) in movies" :key="index"
                 class="flex flex-col justify-between bg-white rounded-md overflow-hidden shadow-md hover:shadow-xl transition-all duration-500 relative">
                <div>
                    <img
                        :src="'https://image.tmdb.org/t/p/w500' + item.backdrop_path"
                         class="transform hover:scale-110 transition-all duration-500 cursor-pointer w-full"
                         alt="test">
                    <div class="p-3 flex flex-col gap-y-4">
                        <div class="flex justify-between">
                            <NuxtLink :to="{ name: 'movie-movieId', params: { movieId: item.id} }" class="text-lg md:text-xl font-bold">
                                {{ item.original_title.slice(0, 20) }}
                                <span v-show="item.original_title.length > 20"> ...</span>
                            </NuxtLink>
                            <span
                                v-click-outside="hideDropdownItems"
                                  class="flex items-center justify-center h-7 w-7 cursor-pointer hover:bg-gray-200 rounded-full relative text-gray-500 hover:text-gray-800"
                                  @click="showDropdownItems(index)">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                                  <path d="M10 6a2 2 0 110-4 2 2 0 010 4zM10 12a2 2 0 110-4 2 2 0 010 4zM10 18a2 2 0 110-4 2 2 0 010 4z" />
                                </svg>
                                <ul v-show="item.showDropDowns" class="flex flex-col rounded-md overflow-hidden bg-gray-200 absolute w-min right-0 top-6 shadow-xl divide-y divide-gray-300 divide-dashed">
                                    <li class="flex items-center gap-x-2 px-3 py-2 hover:bg-gray-300">
                                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 7h.01M7 3h5c.512 0 1.024.195 1.414.586l7 7a2 2 0 010 2.828l-7 7a2 2 0 01-2.828 0l-7-7A1.994 1.994 0 013 12V7a4 4 0 014-4z" />
                                        </svg>
                                        <span>Save</span>
                                    </li>
                                    <li class="flex items-center gap-x-2 px-3 py-2 hover:bg-gray-300">
                                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 21v-4m0 0V5a2 2 0 012-2h6.5l1 1H21l-3 6 3 6h-8.5l-1-1H5a2 2 0 00-2 2zm9-13.5V9" />
                                        </svg>
                                        <span>Report</span>
                                    </li>
                                    <li class="flex items-center gap-x-2 px-3 py-2 hover:bg-gray-300">
                                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5h12M9 3v2m1.048 9.5A18.022 18.022 0 016.412 9m6.088 9h7M11 21l5-10 5 10M12.751 5C11.783 10.77 8.07 15.61 3 18.129" />
                                        </svg>
                                       <span>Subtitle</span>
                                    </li>
                                </ul>
                            </span>
                        </div>
                        <div class="flex items-center gap-x-3 text-gray-700">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                            </svg>
                            <span>{{ item.release_date }}</span>
                        </div>
                        <div class="text-basic text-gray-500 h-24 overflow-hidden">
                            <p>{{ item.overview }}</p>
                        </div>
                    </div>
                </div>
                <span class="p-3 flex gap-x-4 items-center text-gray-600 font-bold bg-gray-100 cursor-pointer">
                    <img src="https://img.icons8.com/color/48/000000/imdb.png" alt=""/>
                    <span class="flex items-center gap-x-2">
                        {{ item.vote_average }}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-yellow-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z" />
                        </svg>
                    </span>

                    <span class="flex items-center gap-x-2">
                        {{ item.vote_count }}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-yellow-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                        </svg>
                    </span>
                </span>

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
import ClickOutside from 'vue-click-outside'

export default {
    name: "AllMovies",
    directives: {
        ClickOutside
    },
    data() {
        return {
            movies: [],
            searchText: ''
        }
    },
    mounted() {
        const self = this;
        this.getMovies()
            .then(res => {
                res.results.forEach(movie => {
                    movie.showDropDowns = false;
                    self.movies.push(movie);
                })
            })
    },
    methods: {
        async getMovies() {
            return await this.$axios.$get('https://api.themoviedb.org/3/movie/now_playing?api_key=bf319d377842d32fdaadacb03d139006');
        },
        showDropdownItems(index) {
            // show one dropdown
            setTimeout(() => {
                this.movies[index].showDropDowns = ! this.movies[index].showDropDowns;
            }, 40)
        },
        hideDropdownItems() {
            // hide all dropdowns
            this.movies.forEach(movie => {
                movie.showDropDowns = false;
            })
        },
        async searchMovies() {
            if (this.searchText) {
                const self = this;
                const moviesInfo = await this.$axios.$get(`https://api.themoviedb.org/3/search/movie?api_key=bf319d377842d32fdaadacb03d139006&page=1&query=${this.searchText}`);
                self.movies = [];
                moviesInfo.results.forEach(movie => {
                    movie.showDropDowns = false;
                    self.movies.push(movie);
                })
            }
        }
    }
}
</script>

<style scoped>
input:focus-visible {
    outline: unset !important;
}
</style>
