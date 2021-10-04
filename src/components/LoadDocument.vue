<template>
    <p>Load one of the existing documents listed below:</p>
    <div class="class-list">
        <div @click="loadDoc(title.title)" class="doc" :key="title" v-for="title in allTitles">
            <p>{{ title.title }}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "LoadDocument",
    emits: ["load-doc"],
    props: {
        allTitles: Array
    },
    methods: {
        loadDoc(title) {
            console.log(title)
            this.$emit("load-doc", title)
        }
    }
}
</script>

<style scoped>
.class-list {
    display: flex;
    flex-direction: column;
    text-align: center;
}

.doc {
    padding: 10px;
    margin: 2px;
    border: 2px solid black;
    border-radius: 5px;
    cursor: pointer;
}
</style>