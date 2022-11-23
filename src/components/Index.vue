<script setup>
import axios from "axios";
import { ref } from "vue";

const selected=ref(null);
const movies=ref(false);

const GetSetData = async () => {
    movies.value= ( 
    await axios.get("https://api.themoviedb.org/3/search/movie", {
        params: {
            api_key: "23b3a0cee96fcac58b28918686474f75",
            include_adult: "true",
            query: selected.value,
        },
    })
    ).data.results[0];
    console.log(movies.value);
};
</script>

<template>
  <div id="searchbar">
    <form action="index.html" method="POST" @submit.prevent="GetSetData">
      <select id="movies" v-model="selected" value="None">
        <option value="None">None</option>
        <option value="Batman">Batman</option>
        <option value="Superman">Superman</option>
        <option value="The Flash">The Flash</option>
        <option value="Wonder Woman">Wonder Woman</option>
        <option value="Green Lantern">Green Lantern</option>
        <option value="Aquaman">Aquaman</option>
        <option value="Joker">Joker</option>
        <option value="Watchmen">Watchmen</option>
        <option value="Catwoman">Catwoman</option>
        <option value="Black Adam">Black Adam</option>
      </select>
      <button type="submit" id="search_btn" @click="GetSetData">Get</button>
    </form>
  </div>
  <div>
    <p class="intro" v-if="movies">
        <br> ID: {{movies.id}}
        <br> Title - {{movies.title}}
        <br> Original Title - {{movies.original_title}}
        <br> Release Date: {{movies.release_date}} 
        <br> Popularity: {{movies.popularity}}               
        <br> Original Language: {{movies.original_language}}
        <br> Vote Count: {{movies.vote_count}}
        <br> Vote Average: {{movies.vote_average}}
        <br> Included Trailer: {{movies.includedTrailer}}
        <br> Adult: {{movies.adult}}
        <br> Overview: {{movies.overview}}
    </p>
    <iframe :src="'https://www.youtube.com/embed/'+{{trailers.at(0).key}}"></iframe>
    <img :src="'https://image.tmdb.org/t/p/w500'+{{movies.poster_path}}" class="image">
  </div>
</template>

<style scoped>
.intro {
  border-radius: 20px;
  height: 500px;
  float: left;
  background-image: linear-gradient(to right, lightgreen, skyblue);
  opacity: 0.9;
  width: 380px;
  color: black;
  padding: 10px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.image {
  float: right;
  border-radius: 40px;
  width: 400px;
  height: 600px;
}

.una {
  border-radius: 20px;
  height: 600px;
  width: 1067px;
  border: 0;
  margin-left: 10px;
}

iframe {
  border-radius: 20px;
  height: 600px;
  border: 0;
  margin-left: 10px;
  aspect-ratio: 16 / 9;
}

body {
  background-image: linear-gradient(lightgrey, whitesmoke) no-repeat;
}

#searchbar {
  display: block;
  margin-right: auto;
  margin-left: auto;
  margin-top: 10px;
  width: 100%;
}

select {
  border-radius: 20px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

button {
  background-image: linear-gradient(to right, lightgreen, skyblue);
  border-radius: 20px;
  border: 0px;
  width: 50px;
  height: 20px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

button:hover {
  background-image: linear-gradient(to right, green, blue);
  color: white;
}

input {
  font-size: 1rem;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

br {
  margin: 0;
}
</style>
