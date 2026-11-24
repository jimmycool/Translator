<template>
    
    <div>
    <textarea rows="4" cols="50" v-model="input1" ></textarea>
    <div>{{ input1 }}</div>
    <br>
    <button   @click="fetch1()">Translate</button>
    <input type="reset"/>
    <div >{{ res }}</div>

    </div>


</template>
<script setup type="module">
import { ref} from 'vue'
//const msg = ref('Welcome to Translato!')
import axios from 'axios';
let res=ref("Hello");
let input1=ref("The weather is very gloomy and dark outside!!");
let options = {
  method: 'POST',
  url: 'https://google-translator9.p.rapidapi.com/v2',
  headers: {
    "Access-Control-Allow-Origin": "*",
    'x-rapidapi-key': '#######################################',
    'x-rapidapi-host': 'google-translator9.p.rapidapi.com',
    'Content-Type': 'application/json'
  },
  data: {
    q:input1.value,
    //q: 'The Great Pyramid of Giza (also known as the Pyramid of Khufu or the Pyramid of Cheops) is the oldest and largest of the three pyramids in the Giza pyramid complex.',
    source: 'en',
    target: 'fr',
    format: 'text'
  }
};
const fetch1= async() =>{

  try {
    options['data'].q=input1.value;
	const response =await  axios.request(options);
	console.log(JSON.stringify(response.data));
  res.value=JSON.stringify(response.data['data']['translations'][0]['translatedText']);
} catch (error) {
	console.error(error);
}
}
</script>