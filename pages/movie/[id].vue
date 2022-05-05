<template>
  <div class="movie">
    <h2>{{ movie.title }}</h2>
    <!-- <h3>{{ $route.params.id }}</h3> -->
    <div class="details">
      <span>{{ movie.release_date }}</span>
      &#8226;
      <span v-for="genre in movie.genres" v-bind:key="genre.name">{{
        genre.name
      }}</span>
      &#8226;
      <span>{{ movie.runtime }} Minutes</span>
    </div>
    <img
      v-bind:src="'https://image.tmdb.org/t/p/w400/' + movie.backdrop_path"
      alt=""
    />
    <h3>{{movie.tagline}}</h3>
    <p>{{movie.overview}}</p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      movie: {},
    };
  },
  created() {
    this.movie.id = this.$route.params.id;
  },
  mounted() {
    getData(
      `https://api.themoviedb.org/3/movie/${this.movie.id}?api_key=48a07cab58fee3df08e3f28be6f3bdbb`,
      (data) => {
        console.log(data);
        this.movie = data;
      }
    );
  },
};
async function getData(url, callback) {
  let rawData = await fetch(url);
  let jsonData = await rawData.json();

  console.log(jsonData);

  callback(jsonData);
}
</script>
<style scoped>
.movie {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 10px;
}
img {
  width: 100%;
}
</style>