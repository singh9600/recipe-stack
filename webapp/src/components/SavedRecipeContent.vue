<template>
    <div class="saved-recipe-content">
        <h4>{{toViewRecipe.title}}</h4>
        <p v-html="toViewRecipe.summary">{{toViewRecipe.summary}}</p>
    </div>
</template>

<script>
export default {
    name: "SavedRecipeContent",
    props: ["toViewRecipe"]
}
</script>

<style scoped>
    .saved-recipe-content {
        padding: 10px;
        background: #f4f4f4;
        border-top: 1px #ccc dotted;
        border-bottom: 2px solid;
    }
    h4 {
        font-weight: 400;
        font-size: 23px;
        border-bottom: 1px #ccc dotted;
        padding-bottom: 10px;
    }
</style>