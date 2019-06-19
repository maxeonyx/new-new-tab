<template>
  <body id="app">
    <header>
      <img id=logo src="./assets/logo.png">
      <nav>
        <div>Home</div>
        <div>Comics</div>
        <div>Programming</div>
      </nav>
    </header>
    <main>
      <div v-for="item in items" :key="item.name" class=bookmark>
        <div class=img :style="'background-image: url(' + item.image + ');'"></div>
        <div class=title>{{item.name}}</div>
      </div>
    </main>
    <footer>

    </footer>
  </body>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      items: [
        {
          name: "Bookmark 1",
          image: "https://i.imgur.com/mV7GwGj.jpg",
        },
        {
          name: "Bookmark 2",
          image: "https://i.imgur.com/mV7GwGj.jpg",
        },
      ],
    };
  },
}
</script>

<style>
html {
  height: 100%;
}
body {
  background-image: url(https://i.imgur.com/mV7GwGj.jpg);
  background-size: 100%;
  padding: 0;
  margin: 0;
  margin-top: 0;
  height: 100%;
  display: flex;
  flex-direction: column;
}

header {
  background-color: rgba(0, 0, 0, 0.7);
  box-shadow: 0 0 3px 3px rgba(0, 0, 0, 0.7);
  display: flex;
  padding: 0.5em;
  flex-direction: row;
  height: calc(3em - 5px);
}

main {
  flex: 1;
  padding-left: 15%;
  padding-right: 15%;
  padding-top: 10%;
  display: grid;
  grid-template-columns: repeat(5, calc(100% / 5));
  grid-auto-rows: 10em;
  grid-auto-flow: row;
}

.bookmark {
  color: lightgray;
  justify-content: center;
  align-content: center;
  background-color: rgba(0, 0, 0, 0.7);
  box-shadow: 2px 2px 5px 5px rgba(0, 0, 0, 0.3);
  margin: 10px;
  cursor: pointer;
  display: flex;
  flex-direction: column;
}
.bookmark:hover {
  position: relative;
  left: 2px;
  top: 2px;
  box-shadow: 1px 1px 3px 3px rgba(0, 0, 0, 0.3);
}

.bookmark .img {
  flex: 1;
  margin: 1px;
  background-repeat: no-repeat;
  background-size: 100%;
}

.bookmark .title {
  font-weight: bold;
  height: 1.3em;
}


footer {
  background-color: rgba(0, 0, 0, 0.7);
  box-shadow: 0 0 5px 5px rgba(0, 0, 0, 0.7);
  height: calc(2em);
}

nav {
  padding-left: 2em;
  flex: 1;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
}

nav div {
  cursor: pointer;
  color: lightgray;
  text-align: center;
  padding: 0.5em;
  padding-left: 1em;
}

#logo {
  height: 3em;
  width: 3em;
}

#app {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#app a {
  display:block;
}

</style>
