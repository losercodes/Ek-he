<template>
  <div>
    <!-- If decodedData is available, render the templates-simple component -->
    <templates-simple v-if="decodedData" :acc="decodedData" />
    
    <!-- If decodedData is not available, show a loading spinner in the center of the screen -->
    <div
      v-else
      class="absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2"
    >
      <base-loading class="h-5 w-5" />
    </div>
  </div>
</template>

<script setup>
import { decodeData } from "../utils/transformer"; // Importing the data decoding utility
const route = useRoute(); // Getting the current route information
const acc = route.query.data; // Extracting 'data' from the query parameters in the route
const decodedData = ref({}); // Declaring a reactive reference for storing decoded data

// Decoding the 'data' parameter and assigning it to decodedData
decodedData.value = decodeData(acc);
</script>
