<template>
    <div class="relative">
        <div class="w-full h-96 overflow-hidden">
            <img :src="HeroImg" alt="alt">
        </div>
        <div class="absolute top-1/2 left-0 w-full h-full">
            <div class="container mx-auto">
                <div class="flex flex-col gap-y-4">
                    <span class="text-red-500 text-basic font-bold">NOW STEAMING</span>
                    <div class="text-white flex"><h4 class="font-bold">NOW </h4> <h4>STREAMING</h4></div>
                    <button class="bg-red-500 px-6 py-3 rounded text-white w-40">View Movies</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import HeroImg from "../../assets/images/movieHero.jpg";

    export default {
        name: "TheHeader",
        data() {
            return {
                HeroImg
            }
        }
    }
</script>

<style scoped>

</style>
