<template>
    <div class="recipe-item">
        <h4>{{generatedRecipe.title}}</h4>
        <p v-html="generatedRecipe.summary">{{generatedRecipe.summary}}</p>
    </div>
</template>

<script>
export default {
    name: "RecipeItem",
    props: ["generatedRecipe"]
}
</script>

<style scoped>
    .recipe-item {
        padding: 10px;
        background: #f4f4f4;
        border-top: 1px #ccc dotted;
    }
    h4 {
        font-weight: 400;
        font-size: 23px;
        border-bottom: 1px #ccc dotted;
        padding-bottom: 10px;
    }
</style>