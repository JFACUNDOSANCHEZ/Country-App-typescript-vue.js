<script setup lang="ts">
 import Pageheader from './components/page/Pageheader.vue'
import CountryList from './components/page/CountryList.vue'
import axios from 'axios'
import { onMounted, ref, watch } from 'vue';
import {Country} from './models/country.model'
const search = ref("")
const countries = ref<Country[]>([])
const filteredCountry = ref<Country[]>([])
const page = ref(1);
const itemsForPage= ref(12)
const paginatedCountry= ref<Country[]>([])
const totalItems = ref(countries.length)
const fetchCountries = async () =>{
try {
  
  const {data} = await axios.get('https://restcountries.com/v3.1//all')
  countries.value=data
  console.log(data);
} catch (error) {
 console.log(error);
  
}
}
  const handleSearch =()=>{
console.log('buscando');
console.log(filteredCountry.value);

filteredCountry.value = countries.value.filter(country =>
        country.name.common.toLowerCase().includes(search.value.toLowerCase())
      );
  }
onMounted(()=>{
  fetchCountries()
  sliceCountry()
})

watch([countries, page], ()=>{
  sliceCountry()
})

const sliceCountry = () => {
  const start = (page.value - 1) * itemsForPage.value;
  const end = start + itemsForPage.value;
  paginatedCountry.value = countries.value.slice(start, end);
};
const changPage =(newpage: number)=>{
  page.value = newpage
}

console.log(page);


</script>


<template>
  
  <Pageheader  />
  <div class="mb-8  flex justify-center">
<input  
v-model="search"
placeholder="search for a country by name"
@input="handleSearch"
type="text" class="border border-blue-700 rounded-xl w-[90%]  px-6 justify-center">
  </div >
  <div class=" text-center  space-x-7 ">
    <button  
    :disabled="page <= 1"
    :class="{'opacity-50': page == 1}"
    @click="$event => changPage(page - 1)"
    class="bg-blue-300 px-5 border border-gray-300 rounded-xl">
      Prev
    </button>
    
    <button 
    :disabled="page >= totalItems"
    :class="{'opacity-50': page >= totalItems}"
    @click="$event=>changPage(page +1) "
    class="bg-blue-300 px-5 border border-gray-300 rounded-xl ">
      next
      
    </button>
  </div>
  <div class="container max-w-screen-lg mx-auto px">
    <CountryList :countries="filteredCountry.length > 0 ? filteredCountry : paginatedCountry"  />
  </div>




</template>

<style scoped>

</style>
