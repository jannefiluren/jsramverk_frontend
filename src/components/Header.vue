<template>
    <h1 id="header">{{ title }}</h1>
</template>

<script>
export default {
    name: "Header",
    props: {
        title: String,
    }
}
</script>

<style scoped>
#header {
    margin-bottom: 20px;
    text-align: center;
}
</style>