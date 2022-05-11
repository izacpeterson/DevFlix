<template>
  <div>
    <div class="intro">
      <h1 class="welcome">Welcome to the club</h1>
      <p>Browse your favorites, discover timeless classics, and find bold new adventures.</p>
      <form action="">
        <input type="text" placeholder="Search...">
        <button>Search</button>
      </form>
    </div>
    <div class="catList">
      <div class="catTitle">
        <h2>Popular Movies</h2>
        <NuxtLink to="/popular">View All</NuxtLink>
      </div>

      <ul>
        <li v-for="movie in popularList" v-bind:key="movie.title">
          <NuxtLink v-bind:to="'/movie/' + movie.id">
            <img v-bind:src="'https://image.tmdb.org/t/p/w200/' + movie.poster_path" alt="" />
            <h3>{{ movie.title }}</h3>
            <h4>{{ movie.release_date }}</h4>

          </NuxtLink>
        </li>
      </ul>
    </div>
    <div class="catList">

      <div class="catTitle">
        <h2>Coming Soon</h2>
        <NuxtLink to="/upcoming">View All</NuxtLink>
      </div>

      <ul>
        <li v-for="movie in upcomingList" v-bind:key="movie.title">
          <NuxtLink v-bind:to="'/movie/' + movie.id" v-if="movie.original_language == 'en'">
            <img v-bind:src="'https://image.tmdb.org/t/p/w200/' + movie.poster_path" alt="" />
            <h3>{{ movie.title }}</h3>
            <h4>{{ movie.release_date }}</h4>

          </NuxtLink>
        </li>
      </ul>
    </div>
    <div class="catList">
      <div class="catTitle">
        <h2>Top Rated</h2>

        <NuxtLink to="/topRated">View All</NuxtLink>
      </div>

      <ul>
        <li v-for="movie in topList" v-bind:key="movie.title">
          <NuxtLink v-bind:to="'/movie/' + movie.id" v-if="movie.original_language == 'en'">
            <img v-bind:src="'https://image.tmdb.org/t/p/w200/' + movie.poster_path" alt="" />
            <h3>{{ movie.title }}</h3>
            <h4>{{ movie.release_date }}</h4>

          </NuxtLink>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      popularList: [],
      topList: [],
      upcomingList: []
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
    getData(
      "https://api.themoviedb.org/3/movie/top_rated?api_key=48a07cab58fee3df08e3f28be6f3bdbb&language=en-US",
      (data) => {
        console.log(data.results);
        this.topList = data.results;
      }
    );
    getData(
      "https://api.themoviedb.org/3/movie/upcoming?api_key=48a07cab58fee3df08e3f28be6f3bdbb&language=en-US",
      (data) => {
        console.log(data.results);
        this.upcomingList = data.results;
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
  flex-direction: row;

  overflow-x: scroll;
  overflow-y: hidden;
  align-items: baseline;
}

li {
  margin: 10px;
  list-style: none;
}

img {
  height: 250px;
  border-radius: 10px;
  box-shadow: 0 0 5px black;

}

select {
  border: none;
  background: none;
  color: white;
  font-size: 32px;
  outline: none;
  text-align: center;
  width: 100%;
}

option {
  background: #111;
  border: none;
  outline: none;
}

a {
  color: white;
  text-decoration: none;
}

h4 {
  font-weight: 100;
}

.welcome {
  font-size: 32px;
}

.intro {
  font-size: 24px;
  padding: 20px;
}

form {
  display: flex;
  padding: 20px 0;
}

form input {
  width: 100%;
}

form button {
  background-color: red;
  color: white;
}

form * {
  border: none;
  font-size: 24px;
  padding: 5px;
  outline: none;
}

.catTitle {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.catTitle a {
  color: red;
  text-decoration: underline;
}
</style>
