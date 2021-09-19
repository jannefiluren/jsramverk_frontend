<template>
  <div class="container">
    <Header :title="'An editor for jsramverk'" />
    <div v-show="showMenu">
      <Button @btn-click="toggleCreateDocument" :text="'Create new document'" :color="'green'" />
      <Button @btn-click="toggleLoadDocument" :text="'Load existing document'" :color="'green'" />
    </div>
    <div v-show="showCreateDocument">
      <CreateDocument @createDoc="createDoc($event)" />
    </div>
    <div v-show="showLoadDocument">
      <LoadDocument @loadDoc="loadDoc($event)" />
    </div>
    <div v-show="showEditor">
      <Editor :doc-title="docTitle" :doc-data="docData" @to-menu="toMenu" :key="docTitle" />
    </div>
  </div>
</template>

<script>
import Editor from "./components/Editor.vue"
import Header from "./components/Header.vue"
import Button from "./components/Button.vue"
import CreateDocument from "./components/CreateDocument.vue"
import LoadDocument from "./components/LoadDocument.vue"

export default {
  name: "App",
  components: {
    Editor,
    Header,
    Button,
    CreateDocument,
    LoadDocument,
  },
  data() {
    return {
      docTitle: "Title from app",
      docData: "<p>String from app...</p>",
      showMenu: true,
      showCreateDocument: false,
      showLoadDocument: false,
      showEditor: false,
    };
  },
  methods: {
    toggleCreateDocument() {
      this.showMenu = false
      this.showCreateDocument = true
      this.showLoadDocument = false
      this.showEditor = false
    },
    toggleLoadDocument() {
      this.showMenu = false
      this.showCreateDocument = false
      this.showLoadDocument = true
      this.showEditor = false
    },
    createDoc(title) {
      this.docTitle = title
      this.docData = "Created a new document..."
      this.showMenu = false
      this.showCreateDocument = false
      this.showLoadDocument = false
      this.showEditor = true
    },
    loadDoc(title) {
      this.docTitle = title;
      this.docData = "Loaded a document..."
      this.showMenu = false
      this.showCreateDocument = false
      this.showLoadDocument = false
      this.showEditor = true
    },
    toMenu() {
      this.showMenu = true
      this.showCreateDocument = false
      this.showLoadDocument = false
      this.showEditor = false
      this.docTitle = ""
      this.docData = ""
    }

  }
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

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
