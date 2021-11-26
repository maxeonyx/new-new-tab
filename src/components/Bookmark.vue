<template>
  <a :href="content.link" class="bookmark">
    <div class="img" :style="'background-image: url(' + content.image + ');'"></div>
    <div class="title">{{content.name}}</div>
  </a>
</template>

<script>
export default {
  props: ["content"]
};
</script>

<style>

.bookmark {
  /* Remove <a> styling */
  outline: 0;
  text-decoration: none;

  border-radius: 10px;

  padding: 0.5em;
  padding-top: 1.5em;
  margin: 10px;

  color: lightgray;
  justify-content: center;
  align-content: center;

  background-color: rgba(0, 0, 0, 0.4);
  box-shadow: 0px 2px 4px 4px rgba(0, 0, 0, 0.25);
  text-shadow: 0 0 3px black, 0 0 3px black, 0 0 5px black, 0 0 7px black;

  display: flex;
  flex-direction: column;

  min-height: 200px;
  min-width: 220px;

  user-select: none;
  
}

.bookmark:hover {
  position: relative;
  top: -2px;
  box-shadow: 0px 5px 6px 6px rgba(0, 0, 0, 0.23);
}

@supports(backdrop-filter: none) {
  .bookmark {
    background-color: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(6px);
    box-shadow: 0px 2px 3px 3px rgba(0, 0, 0, 0.1);
    text-shadow: 0 0 8px black;
  }
  .bookmark:hover {
    background-color: rgba(255, 255, 255, 0.12);
    backdrop-filter: blur(8px);
    box-shadow: 0px 2px 4px 4px rgba(0, 0, 0, 0.06);
  }
}

.bookmark .img {
  flex: 1;
  margin: 1px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
}

.bookmark .title {
  font-weight: bold;
  height: 1.3em;
  margin-top: 0.5em;
}
</style>
