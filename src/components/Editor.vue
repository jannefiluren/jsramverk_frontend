<template>
  <Button @btn-click="logToConsole" :text="'Save'" :color="'blue'" />
  <div id="editor">
    <ckeditor
      :editor="editor"
      v-model="editorData"
      :config="editorConfig"
    ></ckeditor>
  </div>
</template>

<script>
import ClassicEditor from "@ckeditor/ckeditor5-build-classic";
import Button from "./Button.vue";

export default {
  name: "Editor",
  components: {
    Button,
  },
  data() {
    return {
      editor: ClassicEditor,
      editorData: "<p>Start writing here...</p>",
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