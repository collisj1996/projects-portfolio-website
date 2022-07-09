<template>
  <router-view/>
</template>

<style>
@import url('https://fonts.googleapis.com/css?family=Open+Sans');

::-webkit-scrollbar {
  width: 15px;
  height: 15px;
  background-color: transparent;
}

::-webkit-scrollbar-thumb {
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 10px;
}

::-webkit-scrollbar-track {
  background-color: transparent;
}

:root {
  --primary-color: #b7e4c7;
  --secondary-color: #95d5b2;
  --tertiary-color: #74c69d;
}

body {
  margin: 0;
  padding: 0;
  overflow: overlay;
}

#app {
  font-family: 'Open Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #080808;
}
</style>
