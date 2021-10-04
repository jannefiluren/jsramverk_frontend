<template>
  <h3>Document title: {{ docTitle }}</h3>
  <Button @btn-click="saveDoc" :text="'Save'" :color="'blue'" />
  <Button @btn-click="toMenu" :text="'Menu'" :color="'red'" />
  <div id="editor">
    <ckeditor
      :editor="editor"
      v-model="editorData"
      :config="editorConfig"
    ></ckeditor>
  </div>
  <p></p>
</template>

<script>
import ClassicEditor from "@ckeditor/ckeditor5-build-classic";
import Button from "./Button.vue";

const url = window.location.host === "localhost" ? "http://localhost:1337" : "https://jannefilurens-texteditor.azurewebsites.net"

export default {
  name: "Editor",
  emits: ["to-menu"],
  components: {
    Button,
  },
  props: {
    docId: String,
    docTitle: String,
    docText: String,
  },
  data() {
    return {
      editor: ClassicEditor,
      editorData: this.docText,
      editorConfig: {
        config: {
          height: 5000,
        },
      },
    };
  },
  methods: {
    saveDoc() {

      const data = {
        docId: this.docId,
        docTitle: this.docTitle,
        docText: this.editorData,
      };

      fetch(`${url}/update_doc`, {
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
        
    },
    toMenu() {
      this.$emit("to-menu");
    },
  },
};
</script>

<style>
#editor {
  margin-top: 20px;
}

.ck-editor__editable {
  min-height: 500px;
}
</style>