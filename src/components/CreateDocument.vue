<template>
    <form @submit="onSubmit" class="doc-task">
        <div class="form-control">
            <label>Give your new document a title:</label>
            <input type="text" v-model="title">
        </div>
        <input type="submit" value="Create document" class="btn btn-block">
    </form>
</template>


<script>
export default {
    name: "CreateDocument",
    data() {
        return {
            title: "",
        }
    },
    methods: {
        onSubmit(e) {
            e.preventDefault()

            if (!this.title) {
                alert("Please enter a title!")
                return
            }

            this.$emit("create-doc", this.title)
            this.title = ""
        }
    }
}
</script>


<style scoped>
.doc-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>

