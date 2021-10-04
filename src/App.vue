<template>
  <div class="container">
    <Header :title="'An editor for jsramverk'" />
    <div v-show="showMenu" class="menu">
      <Button @btn-click="toggleCreateDocument" :text="'Create new document'" :color="'green'" />
      <Button @btn-click="toggleLoadDocument" :text="'Load existing document'" :color="'green'" />
    </div>
    <div v-show="showCreateDocument">
      <CreateDocument @createDoc="createDoc($event)" />
    </div>
    <div v-show="showLoadDocument">
      <LoadDocument @loadDoc="loadDoc($event)" :all-titles="allTitles" />
    </div>
    <div v-show="showEditor">
      <Editor :doc-id="docId" :doc-title="docTitle" :doc-text="docText" @to-menu="toMenu" :key="docTitle" />
    </div>
  </div>
</template>

<script>
import Editor from "./components/Editor.vue"
import Header from "./components/Header.vue"
import Button from "./components/Button.vue"
import CreateDocument from "./components/CreateDocument.vue"
import LoadDocument from "./components/LoadDocument.vue"

const url = window.location.host === "localhost" ? "http://localhost:1337" : "https://jannefilurens-texteditor.azurewebsites.net"

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
      docId: String,
      docTitle: String,
      docText: String,
      allTitles: Array,
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

      fetch(`${url}/all_titles`)
            .then(res => res.json())
            .then(res => (this.allTitles = res))
            .catch(err => {
                console.error("Error: ", err)
            })

      this.showMenu = false
      this.showCreateDocument = false
      this.showLoadDocument = true
      this.showEditor = false
    },
    createDoc(title) {

      let data = {
        title: title
      }

      fetch(`${url}/insert_doc`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      })
        .then((response) => response.json())
        .then((data) => {
          console.log("Success:", data);
        })
        .catch((error) => {
          console.error("Error:", error);
        });

      this.docTitle = title
      this.docText = "Created a new document..."
      this.showMenu = false
      this.showCreateDocument = false
      this.showLoadDocument = false
      this.showEditor = true

},
    loadDoc(title) {

      fetch(`${url}/read_doc/${title}`)
            .then(res => res.json())
            .then(res => {
              this.docId = res._id;
              this.docTitle = res.title;
              this.docText = res.text;
              this.showMenu = false
              this.showCreateDocument = false
              this.showLoadDocument = false
              this.showEditor = true
            })
            .catch(err => {
                console.error("Error: ", err)
            })
    },
    toMenu() {
      this.showMenu = true
      this.showCreateDocument = false
      this.showLoadDocument = false
      this.showEditor = false
      this.docTitle = ""
      this.docText = ""
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

.menu {
  display: flex;
  justify-content: center;
}
</style>
