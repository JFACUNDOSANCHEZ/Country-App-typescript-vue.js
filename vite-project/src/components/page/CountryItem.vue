<script setup lang="ts">
import { defineProps } from 'vue';
import { Country } from '../../models/country.model';

interface Props {
    country: Country
}

defineProps<Props>()
</script>
<template>
    <div class="text-24  ">
        <img :src="country.flags.png" :alt="country.flags.png" class=" h-56 sm:w-full sm:h-36 ">

        <h3 class="sm:text-4xl text-3xl ">{{ country.name.common }}</h3>
        <p class=" text-gray-500">

            Capital:
        <div v-for="cap in country.capital">

            <span class="font-bold ">
                {{ cap }}

            </span>
        </div>
        </p>
        <p class=" text-gray-500">

            Poblacion:
            <span>

                {{ country.population.toLocaleString() }}
            </span>
        </p>


    </div>
</template>