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

  padding: 0.5em;
  margin: 10px;

  color: lightgray;
  justify-content: center;
  align-content: center;
  background-color: rgba(0, 0, 0, 0.7);
  box-shadow: 2px 2px 5px 5px rgba(0, 0, 0, 0.3);

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
  background-position: center;
  background-size: contain;
}

.bookmark .title {
  font-weight: bold;
  height: 1.3em;
  margin-top: 0.5em;
}
</style>
