<template>
  <div>
    <h2>Movie Page</h2>
    <h3>{{ $route.params.id }}</h3>
  </div>
</template>
<script>
export default {
  data() {
    return {
      movie: {},
    };
  },
  mounted() {
    getData(
      `https://api.themoviedb.org/3/movie/${$route.params.id}?api_key=48a07cab58fee3df08e3f28be6f3bdbb`,
      (data) => {
        console.log(data);
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
