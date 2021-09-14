<template>
  <div class="container">
    <Header v-bind:title="'An editor for jsramverk'" />
    <Editor />
  </div>
</template>

<script>
import Editor from "./components/Editor.vue"
import Header from "./components/Header.vue"

export default {
  name: "App",
  components: {
    Editor,
    Header,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Poppins", sans-serif;
}

.container {
  max-width: 800px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

</style>
