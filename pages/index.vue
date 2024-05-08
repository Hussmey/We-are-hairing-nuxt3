<template>
    <div class="home">
      <Head>
        <Title>Page d'accueil</Title>
      </Head>
      <div class="container mx-auto">
        <div class="max-w-8xl mx-auto">
          <div class="bg-white rounded-lg shadow-lg p-6 h-screen mt-10">
            <h1 class="text-2xl font-semibold mb-4">Création d'une Interface Utilisateur avec Nuxt.js et Tailwind CSS pour l'Intégration d'Offres d'Emploi via une API</h1>
            <h3>Ce court exposé vise à illustrer la manière dont les offres d'emploi peuvent être obtenues à partir d'une API et une interface utilisateur simple peut être créée à l'aide de Nuxt.js et Tailwind CSS.</h3>
  
    <div class="mt-8 py-10 flex flex-wrap justify-center space-x-8 space-y-8">
  <img :src="'/images/nuxt.jpg'" alt="Image 1" class="rounded-full h-40 w-40 mt-5">

  <img :src="'/images/propublic.png'" alt="Image 2" class="rounded-full h-40 w-40 ">

  <img :src="'/images/tailwindcss.png'" alt="Image 3" class="rounded-full h-40 w-40 ">
</div>

<div class="bg-gray-200 rounded-lg p-8">
<h1 class="text-center text-2xl font-semibold">Vous pouvez naviguer vers la pege des offres</h1>

</div>
            <div class="mt-10 flex justify-center">
                
  <button class="transition ease-in-out hover:-translate-y-1 hover:scale-110 duration-300 delay-150 lg:block bg-cyan-500 hover:bg-cyan-700 text-white font-bold py-2 px-4 rounded shadow-sm mt-4">
    <nuxt-link :to="{ name: 'jobs' }">recherchez toutes les offres</nuxt-link>
  </button>
</div>
          </div>
        </div>
      </div>
    </div>
  </template>
  