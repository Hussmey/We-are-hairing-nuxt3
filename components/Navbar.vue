<template>
    <div>
        <nav class="bg-gradient-to-r from-cyan-500 to-blue-500 text-white px-4 py-2 flex items-center">
    <img :src="'/images/propublic.png'" alt="Profil Public Logo" class="w-10 h-10 mr-4 rounded-full" /> 
    <nuxt-link :to="{ name: 'index' }" class="text-xl font-bold mr-4 text-white hover:text-gray-200 active:border-b border-white active:text-underline active:font-bold">Home</nuxt-link>
    <nuxt-link :to="{ name: 'jobs' }" class="text-xl text-white hover:text-gray-200 active:border-b border-white active:text-underline active:font-bold">Jobs</nuxt-link>

    </nav>

    </div>
</template>

<script>
export default {
    mounted() {
        console.log(this.$router.options.routes);
    },
}

</script>