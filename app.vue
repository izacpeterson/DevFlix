<template>
  <div>
    <header>
      <h1>Devflix</h1>
    </header>
    <main>
      <NuxtPage />
    </main>
  </div>
</template>
<style>
* {
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
}

body {
  background-color: #111;
  color: #ddd;
}

header {
  padding: 10px;
  background-color: #222;
  color: red;
  box-shadow: 0 0 5px black;
}

h1 {
  font-size: 24px;
}

main {
  padding: 20px;
}
</style>
