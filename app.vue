<script setup lang="ts">
import { reactive } from 'vue';
//making the options reactive to clicks when clicked
  
import {Gender, Popularity, Length, names} from "@/data"
  
  interface OptionsState {
    gender:Gender;
     popularity: Popularity;
    length: Length;
  }
  // const obt: OptionsState = {
  //   gender:Gender.GIRL,
  //   popularity: Popularity.TRENDY,
  //  length: Length.LONG,
  // };
  const options = reactive<OptionsState>({
    gender:Gender.GIRL,
    popularity: Popularity.TRENDY,
   length: Length.LONG,
  });

  const computeSelectedNames = () => {
    const filteredNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if(options.length === Length.ALL) return true
      else return name.length === options.length
    })
    selectedNames.value = filteredNames.map((name) => name.name)
  }
  const selectedNames = ref<string[]>([])
  const optionsArray = [
    {
      title:"1) Choose a gender",
      category: "gender",
      buttons: [Gender.GIRL, Gender.UNISEX, Gender.BOY]
    },
    {
      title:"1) Choose the name's popularity",
      category: "popularity",
      buttons: [Popularity.TRENDY, Popularity.UNIQUE]
    },
    {
      title:"1) Choose the name's length",
      category: "length",
      buttons: [Length.LONG, Length.ALL, Length.SHORT]
    }
  ]

</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find Names" button below</p>
    <div class="options-container">
      <Option 
      v-for="option in optionsArray"  
      :key="option.title" 
      :option="option" 
      :options="options" />
      <!-- <div class="option-container">
        <h4>1) Choose a gender</h4>
        <div class="option-buttons">
          <button 
          class="option option-left"
          :class="options.gender === Gender.BOY && 'option-active'" 
          @click="options.gender = Gender.BOY">Boy</button>
          <button 
          class="option"
          :class="options.gender === Gender.UNISEX && 'option-active'"
          @click="options.gender = Gender.UNISEX"
          >Unisex</button>
          <button 
          class="option option-right"
          :class="options.gender === Gender.GIRL && 'option-active'"
          @click="options.gender = Gender.GIRL"
          >Girl</button>
        </div>
      </div>
      <div class="option-container">
        <h4>2) Choose the name's popularity</h4>
        <div class="option-buttons">
          <button 
          class="option option-left"
          :class="options.popularity === Popularity.TRENDY && 'option-active'"
          @click="options.popularity = Popularity.TRENDY"
          >Trendy</button>
          <button 
          class="option option-right"
          :class="options.popularity === Popularity.UNIQUE && 'option-active'"
          @click="options.popularity = Popularity.UNIQUE"
          >Unique</button>
        </div>
      </div>
      <div class="option-container">
        <h4>3) Choose name's length</h4>
        <div class="option-buttons">
          <button 
          class="option option-left "
          :class="options.length === Length.LONG && 'option-active'"
          @click="options.length = Length.LONG"
          >Long</button>
          <button 
          class="option"
          :class="options.length ===Length.ALL && 'option-active'"
          @click="options.length = Length.ALL"
          >All</button>
          <button 
          class="option option-right"
          :class="options.length === Length.SHORT && 'option-active'"
          @click="options.length = Length.SHORT"
          >Short</button>
        </div>
      </div> -->
      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>
    <div class="cards-container">
      <div v-for="name in selectedNames" :key="name" class="card">
        <h4>{{ name }}</h4>
        <p>x</p>
      </div>
    </div> 
  </div>
  
</template>
<style scoped>
  .container{
    font-family: Arial, Helvetica, sans-serif;
    color: rgb(27, 60, 138);
    max-width: 50rem;
    margin: 0 auto;
    text-align: center;
  }
  h1{
     font-size: 3rem;
  }
  .options-container{
    background-color: rgb(255, 238, 236);
    border-radius: 2rem;
    padding: 1rem;
    width: 95%;
    margin: 0 auto;
    margin-top: 4rem;
    position: relative;
  }
  .primary{
    background-color: rgb(249, 87, 89);
    color: white;
    border-radius: 6.5rem;
    border: none;
    padding: 0.75rem 4rem;
    margin-top: 1rem;
    font-size: 1rem;
    cursor: pointer;
  }
  .cards-container{
    display: flex;
    margin-top: 3rem;
    flex-wrap: wrap;
  }
  .card{
    background-color: rgb(27,60,138);
    width: 28%;
    height: 20px;
    color: white;
    border-radius: 1rem;
    padding: 1rem;
    margin-right: 0.5rem;
    margin-bottom: 1rem;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;

  }

  .card p{
    position: absolute;
    top: -30%;
    left: 92.5%;
    cursor: pointer;
    color: rgba(255, 255, 255, 0.178 );
  }
</style>
