<template>
    <div class="w-full h-full bg-gray-200">
        <!-- the header -->
        <TheHeader />

        <!-- all movies -->
        <AllMovies />
    </div>
</template>

<script>
import TheHeader from "~/components/Templates/TheHeader";

export default {
        name: 'IndexPage',
        components: {
            TheHeader
        },
    }
</script>

<style>

</style>
