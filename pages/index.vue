<template>
  <div>
    <select>
      <option value="">Popular Movies</option>
      <option value="">Latest Movies</option>
      <option value="">Top Rated</option>
    </select>
    <ul>
      <li v-for="movie in popularList" v-bind:key="movie.title">
        <NuxtLink v-bind:to="'/movie/' + movie.id">
          <h3>{{ movie.title }}</h3>
          <img
            v-bind:src="'https://image.tmdb.org/t/p/w200/' + movie.poster_path"
            alt=""
          />
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      popularList: [],
    };
  },
  mounted() {
    getData(
      "https://api.themoviedb.org/3/movie/popular?api_key=48a07cab58fee3df08e3f28be6f3bdbb",
      (data) => {
        console.log(data.results);
        this.popularList = data.results;
      }
    );
  },
};

async function getData(url, callback) {
  let rawData = await fetch(url);
  let jsonData = await rawData.json();

  callback(jsonData);
}
</script>
<style>
ul {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
select{
  border: none;
  background: none;
  color:white ;
  font-size: 32px;
  outline: none;
  text-align: center;
  width: 100%;
}
option{
  background: #111;
  border: none;
  outline: none;
}
</style>
