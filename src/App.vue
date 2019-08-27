<template>
<body id="app" :style="body_style">
  <header>
    <img id="logo" src="./assets/logo.png" />
    <nav>
      <div
        v-for="tab in tabs"
        :key="tab.name"
        :class="'tab ' + (current_tab === tab.name ? 'selected' : '')"
        @click="change_tab(tab.name)"
      >{{ tab.name }}</div>
      <div class="filler" />
      <div
        class="tab editor"
        :class="current_tab === 'Editor' ? 'selected' : ''"
        @click="change_tab('Editor')"
      >Editor</div>
    </nav>
  </header>
  <main>
    <Tab v-for="tab in tabs" v-show="current_tab === tab.name" :key="tab.name" :content="tab" />
    <Editor v-show="current_tab === 'Editor'" v-on:input="updateData" />
  </main>
  <footer></footer>
</body>
</template>

<script>
import Editor from "./components/Editor";
import Tab from "./components/Tab";

export default {
  name: "app",
  data() {
    return {
      current_tab: "Home",
      app_data: null
    };
  },
  computed: {
    tabs() {
      if (!this.app_data) return [];
      if (!this.app_data.tabs) return [];

      return Object.keys(this.app_data.tabs).map(name => ({
        name,
        ...this.app_data.tabs[name]
      }));
    },
    body_style() {
      if (!this.app_data) return "";
      if (!this.app_data.background_image) return "";

      return "background-image: url(" + this.app_data.background_image + ");";
    }
  },
  methods: {
    change_tab(tab_name) {
      this.current_tab = tab_name;
    },
    updateData(data) {
      this.app_data = data;
    }
  },
  components: {
    Tab,
    Editor
  }
};
</script>

<style>
html {
  height: 100%;
}
body {
  background-image: url(https://i.imgur.com/mV7GwGj.jpg);
  background-size: min(auto, 100vw) min(auto, 100vh);
  padding: 0;
  margin: 0;
  margin-top: 0;
  height: 100%;
  display: flex;
  flex-direction: column;
}

header {
  background-color: rgba(0, 0, 0, 0.7);
  box-shadow: 0 0 2px 2px rgba(0, 0, 0, 0.7);
  display: flex;
  padding: 0.5em;
  flex-direction: row;
}

footer {
  background-color: rgba(0, 0, 0, 0.7);
  box-shadow: 0 0 2px 2px rgba(0, 0, 0, 0.7);
  height: calc(2em);
}

main {
  flex: 1;
  margin-left: 5vw;
  margin-right: 5vw;
  margin-top: 5vh;
  margin-bottom: 5vh;
}

@media (max-width: 450px) {
  .bookmark {
    width: 100%;
    height: 100px;
  }
}
@media (min-width: 450px) {
  .bookmark {
    min-height: 200px;
    min-width: 380px;
  }
}

.tab-content {
  display: flex;
  flex-direction: row;
  justify-content: center;
  flex-wrap: wrap;
  width: 100%;
}

nav {
  padding-left: 2em;
  flex: 1;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
}

nav .tab {
  cursor: pointer;
  color: lightgray;
  text-align: center;
  padding: 0.5em;
  margin-left: 1em;

  /* transparent border when not selected means the element doesn't change size when selected */
  border-bottom: 3px solid rgba(0, 0, 0, 0);
}

nav div.selected {
  border-bottom: 3px solid white;
}

nav div.filler {
  flex: 1;
}

nav div.editor {
  justify-self: flex-end;
}

#logo {
  height: 3em;
}

#app {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
