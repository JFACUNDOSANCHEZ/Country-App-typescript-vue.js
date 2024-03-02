<script setup lang="ts">
import { defineProps } from 'vue';
import { Country } from '../../models/country.model';
import CountryItem from '../page/CountryItem.vue'

interface Props {
    countries: Country[]
}

defineProps<Props>()
</script>


<template>


    <div class="grid  grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-3 w-full p-6  ">
     
        <div v-for="country in countries"  class="border bg-white border-gray-500 rounded-xl p-3">
<CountryItem  :country="country" />

    </div>
</div>
</template>