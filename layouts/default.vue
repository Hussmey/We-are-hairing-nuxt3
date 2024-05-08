<template>
    <div class="h-screen min-h-screen flex flex-col">
      <Navbar />
      <slot class="py-4 flex-auto" />  <Footer class="flex-grow" />
    </div>
  </template>
  
  <script>
  import Navbar from '~/components/Navbar.vue';
  import Footer from '~/components/Footer.vue';
  
  export default {
    components: {
      Navbar,
      Footer,
    },
  };
  </script>