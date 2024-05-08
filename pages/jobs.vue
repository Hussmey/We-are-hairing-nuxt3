<template>
     <Head>
            <Title > Offres d'emploi</Title>
        </Head>
  <div class="bg-gray-200 p-4 mt-6">
    <div class="container mx-auto">
      <div class="grid grid-cols-12 gap-1">
        <div class="col-span-12 lg:col-span-4 bg-gray-200 p-4 card-wrapper">
          <div
           v-for="item in filteredData" 
          :key="item.id"
           class="job-card bg-white rounded-lg shadow-md p-4 flex flex-col items-start justify-between mb-4"  
          :class="{ 'border-4 border-cyan-400 bg-cyan-25': activeItem === item.id }" >

            <div class="job-details w-full" >
              <div class="flex justify-between">
                <div class="py-2">
                  <h2 class="job-title text-x2 font-medium">{{ item.title }}</h2>
                  <p class="job-company text-gray-700">{{ item.company }}</p>
                </div>
                <div class="flex items-center">
                  <div class="flex items-center bg-cyan-500 text-white rounded-full px-2">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/>
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14a6 6 0 016-6M4 14a6 6 0 016-6m-3 8v2m0 0v2m0-2h2m-2 0H7"/>
                    </svg>
                    {{ item.viewCount }} 
                  </div>
                </div>
              </div>
            </div>
            <div class="job-description text-gray-600 mt-2">{{ item.answer2.slice(0, 225) }}</div>
            <div class="job-details w-full mt-5">
              <div class="flex justify-between">
                <div class="flex flex-col items-center text-left">
                  <h5 class="text-gray-400">{{ formatRelativeTime(item.submittedAt) }}</h5>
                  <h5 class="text-left text-gray-600">{{ item.type === 'public' ? 'cdi/cdd/internship' : item.type }}</h5>
                </div>
                <button @click="showOffcanvas(item)" 
                class="transition ease-in-out hover:-translate-y-1 hover:scale-110  duration-300 delay-150 hidden lg:block bg-cyan-400 hover:bg-cyan-700 text-white font-bold py-2 px-4 rounded shadow-sm mt-4">Voir plus</button>
               <button @click="showOffcanvasResponsive(item)" 
                class="lg:hidden bg-cyan-400 hover:bg-cyan-700 text-white font-bold py-2 px-4 rounded shadow-sm mt-4">Voir plus</button>
              </div>
            </div>
          </div>
        </div>
        
        <div class="hidden lg:block bg-white rounded-lg shadow-md col-span-8 lg:col-span-8 bg-gray-300 p-4 mt-4 h-dvh sticky top-0"  v-if="selectedItem">
    <div class="bg-gray-200 rounded-lg p-2">
      <div class="flex justify-between">
      <div class="flex justify-start items-center"> 
        <span class="font-medium ">salaries :</span> <span v-if="selectedItem.salaryMin !== null && selectedItem.salaryMin !== 0">à partir de</span> {{ selectedItem.salaryMin }} {{ salaryPeriodText }}
      </div>
      <span>{{ formattedDate(selectedItem.createdAt) }}</span>
    </div>
    </div>
    <div class="p-2 border-b-4 border-gray-300 mt-7">
    <div class="flex items-center">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-600 mr-2" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M3.5 5a.5.5 0 0 1 .5-.5h12a.5.5 0 0 1 0 1h-12a.5.5 0 0 1-.5-.5zM5 6a1 1 0 1 0-2 0v8a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V6a1 1 0 1 0-2 0v8a1 1 0 0 1-1 1H6a1 1 0 0 1-1-1V6zm8-2.5a.5.5 0 0 1 .5-.5h1a.5.5 0 0 1 0 1h-1a.5.5 0 0 1-.5-.5zM5 6.5a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 .5.5v8a.5.5 0 0 1-.5.5H5a.5.5 0 0 1-.5-.5v-8zM7 8a1 1 0 0 1 2 0v4a1 1 0 0 1-2 0V8zm4 0a1 1 0 0 1 2 0v4a1 1 0 0 1-2 0V8z" clip-rule="evenodd"/>
      </svg>
      <h3 class="font-semibold pr-5">Type d'emploi:</h3>  <h5 class="text-left text-gray-600">{{ selectedItem.type === 'public' ? 'cdi/cdd/internship' : selectedItem.type }}</h5>
    </div>
    <div class="flex items-center mt-3">
    <svg
      v-if="selectedItem.expiresAt"
      xmlns="http://www.w3.org/2000/svg"
      class="h-6 w-6 text-gray-600 mr-2"
      viewBox="0 0 20 20"
      fill="currentColor"
    >
      <path
        fill-rule="evenodd"
        d="M10 18a8 8 0 1 0 0-16 8 8 0 0 0 0 16zM11 11a1 1 0 0 0 1.732-.732l1.5-6a1 1 0 1 0-1.932-.536L11 10.268V6a1 1 0 0 0-2 0v5.268a1 1 0 0 0 .5.866l1 5a1 1 0 0 0 .932.732 1 1 0 0 0 .932-.732l1-5a1 1 0 0 0 .5-.866V6a1 1 0 0 0-2 0v4.268l-.5-.268-1.5 6A1 1 0 0 0 11 11z"
        clip-rule="evenodd"
      />
    </svg>
      <h3 class="font-semibold pr-5">Adapter à :</h3>
      <div class="bg-green-300 rounded-lg p-2"  :class="{ 'bg-green-300': isDateValid(selectedItem.expiresAt), 'bg-red-300': !isDateValid(selectedItem.expiresAt) }">
         <h5 class="text-left text-gray-600">{{ selectedItem.expiresAt }}</h5>
      </div>
  </div>
  </div>

  <div class=" mt-5 ps-2">
    <h1 class="text-lg font-semibold underline">Description complète du poste</h1>
    <div class="mt-5">
    <h2 class="text-lg text-center font-semibold mb-2">{{ selectedItem.title }}</h2>
    <p class="py-2">{{ selectedItem.answer1 }}</p>
    <p class="py-2">{{ selectedItem.answer2 }}</p>
    <p class="py-2">{{ selectedItem.answer3 }}</p>
    </div>
  </div>
  <div class="mt-5 flex justify-center">
  <button class="transition ease-in-out hover:-translate-y-1 hover:scale-110 duration-300 delay-150 lg:block bg-cyan-400 hover:bg-cyan-700 text-white font-bold py-2 px-4 rounded shadow-sm mt-4">
    <a href="https://profilpublic.fr/jobs" target="_blank">Postuler maintenant</a>
  </button>
</div>


  </div>
  <div v-else class="hidden lg:block bg-white rounded-lg shadow-md col-span-8 lg:col-span-8 bg-gray-300 p-4 max-h-80 mt-4 sticky top-0">
    <p>No data available</p>
  </div>
        <div class="offcanvas lg:hidden" v-if="selectedItemresponsive">
          <div class="offcanvas-content bg-white rounded-lg shadow-md p-4">
            <button @click="closeOffcanvas" class="close-button bg-red-400 hover:bg-red-700 text-white font-bold py-2 px-4 rounded shadow-sm mt-4">Close</button>
            <h2 class="text-lg font-semibold mb-2">{{ selectedItemresponsive.title }}</h2>
            <p>{{ selectedItemresponsive.answer2 }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref,computed  } from 'vue';
import axios from 'axios';
import { formatDistanceToNow } from 'date-fns';

const result = await axios.get('https://app.staging.profilpublic.fr/api/jobs').then((response) => response.data);

const selectedItem = ref(null);
const selectedItemresponsive = ref(null);
const activeItem = ref(null);


const filteredData = result.data.filter(item => item.answer2 !== null);

const formatRelativeTime = (timestamp) => {
  if (!timestamp) return '';
  const now = new Date();
  const submittedAt = new Date(timestamp);
  return formatDistanceToNow(submittedAt, { addSuffix: true });
};

const isDateValid = (expiresAt) => {
  if (!expiresAt) return false;
  const expirationDate = new Date(expiresAt);
  const currentDate = new Date();
  return expirationDate >= currentDate;
};

const showOffcanvas = (item) => {
  selectedItem.value = item;
  activeItem.value = item.id;
  document.body.classList.add('offcanvas-open');
};

const showOffcanvasResponsive = (item) => {
  const screenWidth = window.innerWidth;
  if (screenWidth < 1024) { 
    selectedItemresponsive.value = item;
    activeItem.value = item.id;
    document.body.classList.add('offcanvas-open');
  }
};


const closeOffcanvas = () => {
  selectedItemresponsive.value = null;
  document.body.classList.remove('offcanvas-open');
};

const salaryPeriodText = computed(() => {
  const selectedItemValue = selectedItem.value;
  if (!selectedItemValue || !selectedItemValue.salaryPeriod) return "Lore de l'entretien";
  const { salaryMin, salaryPeriod } = selectedItemValue;
  
  if (salaryMin === 0) return "Lore de l'entretien"; // Handle scenario where salaryMin is 0
  
  if (salaryPeriod.toLowerCase() === 'month') return 'Mensuel';
  else if (salaryPeriod.toLowerCase() === 'year') return 'Annuel';
  else return salaryMin;
});

const formattedDate = (timestamp) => {
  if (!timestamp) return '';
  const date = new Date(timestamp);
  const formattedDateString = `${date.getFullYear()}-${(date.getMonth() + 1).toString().padStart(2, '0')}-${date.getDate().toString().padStart(2, '0')} ${date.getHours().toString().padStart(2, '0')}h:${date.getMinutes().toString().padStart(2, '0')}`;
  return formattedDateString;
};

const goToJobsPage = () => {
  window.location.href = 'https://profilpublic.fr/jobs';
};
</script>

<style scoped>
.offcanvas {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 999;
  display: flex;
  align-items: center;
  justify-content: center;
}

.offcanvas-content {
  max-width: 90%;
  max-height: 90%;
  overflow-y: auto;
}

.close-button {
  position: absolute;
  top: 260px;
  right: 10px;
}
</style>
