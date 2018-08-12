<template>
    <div>
         <span id="title">{{ title }}:</span> {{ value }}
    </div>
</template>

<script>
export default {
    name: "ResultItem",
    props: {
        title: String,
        value: String
    }
}
</script>

<style scoped>
    div {
        margin-bottom: 10px;
    }

    div #title {
        font-weight: bolder;
    }
</style>