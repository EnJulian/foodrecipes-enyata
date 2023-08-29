<script setup xmlns="http://www.w3.org/1999/html">
import {onUpdated, ref} from "vue";
import axios from "axios";
import {useRouter} from "vue-router";

const router = useRouter();
const meals = ref([]);
const mealName = ref("");
async function fetchData(){
  try {
    const response = await axios.get("https://themealdb.com/api/json/v1/1/search.php?s=" + mealName.value )
    meals.value = response.data.meals
  }
  catch (error){
    console.log(error)
  }
}
fetchData();
onUpdated(()=>{fetchData()})
</script>

<template>
<!--V-model for only input texts-->
  <main>
    
    
    <div class="list-view">
      <img class="union" src="src/assets/union.svg" alt="">
      <nav class="nav-bar">
        <img class="foodl" src="src/assets/foodl.svg" alt="">
        <span class="nav-item-right">Home</span>
        <span class="nav-item-right">Search</span>
      </nav>
      <h1 class="header">What ingredients do you have?</h1>
            <div class="input-with-icon">
              <img class="input-icon" src="src/assets/charm-search.svg" />
              <input type="text" v-model="mealName" class="rectangle" placeholder="Enter food name">
            </div>
          <div class="group-2"></div>
         
          
        
      
    </div>
    
    
  <div class="card-outer">
    <div @click="router.push({name:'recipe', params:{name:meal.strMeal}})" v-for="meal in meals" class="card">
      <img :src="meal.strMealThumb" :alt="meal.strMeal" class="card-image">
      <p> {{meal.strMeal}} </p>
    </div>
  </div>
</main>
</template>

<style scoped>
main{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 0;
}

.card-outer {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 120px;
  padding: 10px;
}

.card {
  border: none;
  border-radius: 16px;
  background: #FFF;
  box-shadow: 0px 24px 64px -16px rgba(0, 0, 0, 0.10);
  padding: 10px;
  text-align: center;
  width: 285px;
  height: 270px;
  flex-shrink: 0;
}
.card-image{
  border-radius: 8px;
  box-shadow: 0px 32px 48px -16px rgba(0, 0, 0, 0.25);
  width: 248px;
  height: 229px;
  flex-shrink: 0;
}


input:focus,
textarea:focus,
select:focus {
  outline: none;
}


.list-view {
  background: #F9A263;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding-bottom: 150px;
  width: 100%;
}

.union{
  display: flex;
  position: absolute;
  left: 85%;
  top: 10px;
}

.nav-bar{
  display: flex;
  align-items: center;
}
nav img{
  margin-right: 1500px;
}

nav span{
  display: flex;
  margin: auto 20px;
  font-family: "IBM Plex Sans-Bold", Helvetica;
  font-weight: 700;
  color: #000000;
  font-size: 18px;
  letter-spacing: -0.72px;
  line-height: 23.4px;
  white-space: nowrap;
}
.list-view .input-with-icon {
  width: 590px;
  position: relative;
  top: 90px;
  height: 64px;
  background-color: #fbfbfb;
  border-radius: 16px;
  box-shadow: 0px 32px 40px -16px #b5530d66;
}

.input-with-icon input{
  display: flex;
  text-align: center;
}

.list-view .rectangle {
  width: 590px;
  height: 52px;
  background-color: #ffffff;
  border: none;
  border-radius: 11px;
  box-shadow: 0px 20px 24px -8px #b5530d1c;
}


.list-view .input-icon {
  position: absolute;
  top: 40%;
  left: 10px;
  transform: translateY(-50%);
}


.list-view .header {
  font-family: "IBM Plex Sans-Bold", Helvetica;
  font-weight: 700;
  position: relative;
  top: 80px;
  color: #000000;
  font-size: 32px;
  letter-spacing: -1.28px;
  line-height: 32px;
  white-space: nowrap;
}

</style>
