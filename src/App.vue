<template>
<body id="app" :style="body_style">
  <header>
    <img id="logo" src="/logo.png" />
    <nav>
      <div
        v-for="tab in tabs"
        :key="tab.name"
        :class="'tab ' + (current_tab === tab.name ? 'selected' : '')"
        @click="change_tab(tab.name)"
      >{{ tab.name }}</div>
      <div class="filler"></div>
      <div class="tab"><a target="_blank" href="https://gist.github.com/maxeonyx/fa60371050c93cc141fc0b2086bec30f/edit">Edit</a></div>
      <img  class="tab refresh" src="/refresh.svg" 
        @click="reloadGistData()" />
    </nav>
  </header>
  <main>
    <Tab v-for="tab in tabs" v-show="current_tab === tab.name" :key="tab.name" :content="tab" />
    <div v-show="profile === null" class=tab-content>
      <div v-for="profile in profiles" @click="setProfile(profile)" class="bookmark">
        <div class="img"></div>
        <div class="title" >{{profile}}</div>
      </div>
    </div>
  </main>
</body>
</template>

<script>
import Tab from "./components/Tab";

export default {
  name: "app",
  data() {
    return {
      profile: null,
      profiles: [],
      current_tab: null,
      app_data: null,
      text: "",
    };
  },
  created() {
    this.profile = localStorage.getItem('profile');
    this.app_data = JSON.parse(localStorage.getItem('app_data'));
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
  watch: {
    app_data() {
      if (this.app_data) {
        localStorage.setItem('app_data', JSON.stringify(this.app_data));
        if (this.current_tab === null) {
          if (Object.keys(this.app_data.tabs).length > 0) {
            this.current_tab = Object.keys(this.app_data.tabs)[0];
          }
        }
      }
    }
  },
  methods: {
    change_tab(tab_name) {
      this.current_tab = tab_name;
    },
    updateData(data) {
      this.app_data = data;
    },
    async get_gist() {
      let response = await fetch('https://api.github.com/gists/fa60371050c93cc141fc0b2086bec30f');
      let data = await response.json();
      let files = {};
      for (let filename of Object.keys(data.files)) {
        let f = data.files[filename];
        try {
          files[filename] = JSON.parse(f.content);
        } catch {
          console.log("Failed to parse " + filename);
        }
      }
      this.profiles = Object.keys(files);
      return files;
    },
    async reloadGistData() {
      let files = await this.get_gist();
      this.app_data = files[this.profile];
    },
    async setProfile(profile) {
      this.profile = profile;
      localStorage.setItem('profile', this.profile);
      await this.reloadGistData();
    }
  },
  components: {
    Tab
  }
};
</script>

<style>
html {
  height: 100%;
}
body {
  background-image: url(/background.jpg);
  background-position: center;
  background-size: cover;
  padding: 0;
  margin: 0;
  margin-top: 0;
  height: 100%;
  display: flex;
  flex-direction: column;
}

header {
  background-color: rgba(0, 0, 0, 0.4);
  box-shadow: 0px 0px 4px 4px rgba(0, 0, 0, 0.25);
  text-shadow: 0 0 5px black, 0 0 5px black, 0 0 5px black, 0 0 7px black;
  display: flex;
  padding: 0.5em;
  flex-direction: row;

  user-select: none;
}

@supports(backdrop-filter: none) {
  header {
    backdrop-filter: blur(6px);
    background-color: rgba(255, 255, 255, 0.1);
    box-shadow: 0 0 2px 2px rgba(0, 0, 0, 0.2);
    text-shadow: 0 0 5px black, 0 0 7px black;
  }
}

main {
  flex: 1;
  margin-left: 5vw;
  margin-right: 5vw;
  margin-top: 5vh;
  margin-bottom: 5vh;
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

nav .tab a {
  color: inherit;
  text-decoration: none;
}

nav .tab:hover {
  border-bottom: 3px solid rgba(255, 255, 255, 0.3);
}

nav .refresh {
  height: 1.2em;
  width: 1.2em;
}

nav .tab.selected {
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
