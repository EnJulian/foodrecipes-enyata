<script setup>
import {useRoute} from "vue-router";
import axios from "axios";
import {computed, ref} from "vue";  

const route = useRoute();
const meals = ref([]);
async function fetchData(){
  try {
    const response = await axios.get("https://themealdb.com/api/json/v1/1/search.php?s=" + route.params.name )
    meals.value = response.data.meals
  }
  catch (error){
    console.log(error)
  }
}
fetchData();
const instructions = computed(()=>{return meals.value[0].strInstructions.split("\r\n")})
</script>

<template>
  <div>
    <img :src="meals[0].strMealThumb" alt=""> 
  </div>
<p>{{meals[0].strMeal}}</p>
  
  <p v-for="instruction in instructions">{{instruction}}</p>
</template>

<style scoped>

</style>
