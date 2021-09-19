<template>
    <!-- <ul>
        <li :key="doc.title" v-for="doc in docs">
        {{ doc.title }}
        </li>
    </ul> -->
    <p>Load one of the existing documents listed below:</p>
    <div class="class-list">
        <div @click="loadDoc(doc.title)" class="doc" :key="doc.title" v-for="doc in docs">
            <p>{{ doc.title }}</p>
        </div>
    </div>

</template>

<script>
export default {
    name: "LoadDocument",
    emits: ["load-doc"],
    data() {
        return {
            docs: [
                {
                    title: "Doc 1",
                    text: "Text 1",
                },
                {
                    title: "Doc 2",
                    text: "Text 2",
                },
                {
                    title: "Doc 3",
                    text: "Text 3",
                },
            ]
        }
        
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