<script setup>
 import { ref } from 'vue'
 import axios from "axios";

 const movieIMG = ref(null);
 const movieTitle = ref(null);
 const budget = ref(null);
 const language = ref(null);
 const poster = ref(null);
 const overview = ref(null);
 const genre = ref(null);
 const company = ref(null);
 const date = ref(null);
 const revenue = ref(null);
 const trailers = ref(null);

 function displayMovie() {

  let movie_id = document.getElementById("movieOptions").value;

  let getRequest = axios.get(`https://api.themoviedb.org/3/movie/${movie_id}`, {
    params: {
      api_key: "49468aca2342aec8c99327aff8518492",
      append_to_response: "videos",
    },
  });

 getRequest.then((finalResult) => {
    movieIMG.value.style.backgroundImage = `url(https://image.tmdb.org/t/p/w500/${finalResult.data.backdrop_path})`;
    movieTitle.value = finalResult.data.original_title;
    budget.value = "Budget: $" + finalResult.data.budget;
    language.value = "Language: " + finalResult.data.original_language;
    poster.value = "https://image.tmdb.org/t/p/w500" + finalResult.data.poster_path;
    overview.value = "Overview: " + finalResult.data.overview;
    genre.value = "Genre: " + finalResult.data.genres[1].name;
    company.value = "Company: " + finalResult.data.production_companies[0].name;
    date.value = "Release Date: " + finalResult.data.release_date;
    revenue.value = "Revenue: $" + finalResult.data.revenue;
    trailers.value = "https://www.youtube.com/embed/" + (finalResult.data.videos.results.filter((trailer) => trailer.type === "Trailer")).at(0).key});
}
</script>

<template>
 <select name="movieNames" id="movieOptions">
      <option value="245891">John Wick</option>
      <option value="19995">Avatar</option>
      <option value="157336">interstellar</option>
      <option value="129">Spirited Away</option>
      <option value="497">The Green Mile</option>
      <option value="423">The Pianist</option>
      <option value="8587">The Lion King</option>
      <option value="718930">Bullet Train</option>
      <option value="354912">Coco</option>
      <option value="68718">Django</option>
    </select>
    <button @click="displayMovie()">Get</button>

    <div id="backIMG" ref="movieIMG"></div>

    <p id="movieTitle">{{movieTitle}}</p>
    <img id="poster" :src="poster"/>
    <iframe id="trailers" :src="trailers"></iframe>
    <div class="info">
      <p id="budget" >{{budget}}</p>
      <p id="revenue">{{revenue}}</p>
      <p id="company">{{company}}</p>
      <p id="date">{{date}}</p>
      <p id="genre">{{genre}}</p>
      <p id="language">{{language}}</p>
    </div>
    <p id="overview">{{overview}}</p>
</template>

<style scoped>

#poster {
    width: 300px;
    height: 450px;
    margin-right:29%;
}

#trailers {
    width: 750px;
    height: 450px;
}

body{
    background-color: black;
    font-size: 20px;
    color: beige;
    font-family: "courier new";
}
#backIMG{
    position: absolute;
    background-image: url(https://image.tmdb.org/t/p/w500/ff2ti5DkA9UYLzyqhQfI2kZqEuh.jpg) no-repeat center;
    background-size: cover;

    background-color: darkgrey;
    filter: brightness(30%);
    opacity: 40%;
    z-index: -1;

    width: 99%;
    height: 99%;
    top:0%;

}

#movieTitle{
    font-weight: bold;
    font-size: 24px;
}

.info{
    line-height: 3;
    position:absolute;
    padding-left: 22%;
    top: 10%;
}

#overview{
    font-size: 18px;
    position: absolute;
    top: 74%;
    width: 740px;
}

</style>
