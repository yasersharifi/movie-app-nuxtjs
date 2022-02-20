<template>
    <div class="w-full h-full bg-gray-200">
        <!-- the header -->
        <TheHeader />

        <Nuxt />
    </div>
</template>

<script>
    import TheHeader from "~/components/Templates/TheHeader";
    export default {
        name: "default",
        components: {TheHeader}
    }
</script>

<style scoped>

</style>
