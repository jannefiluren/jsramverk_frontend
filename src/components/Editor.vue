<template>
  <h3>Document title: {{ docTitle }}</h3>
  <Button @btn-click="logToConsole" :text="'Save'" :color="'blue'" />
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

export default {
  name: "Editor",
  emits: ['to-menu'],
  components: {
    Button,
  },
  props: {
    docTitle: String,
    docData: String,
  },
  data() {
    return {
      editor: ClassicEditor,
      editorData: this.docData,
      editorConfig: {
        config: {
          height: 5000,
        },
      },
    };
  },
  methods: {
    logToConsole() {
      console.log(this.editorData);
    },
    toMenu() {
      this.$emit("to-menu")
    }
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