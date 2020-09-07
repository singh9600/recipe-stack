<template>
    <div class="saved-recipe-item">
        <p>
            {{savedRecipie.title}}
            <button @click="$emit('del-recipe', savedRecipie.recipeID)" class="del"> delete </button>
            <button @click="$emit('view-recipe', savedRecipie.recipeID)" class="view"> view </button>
        </p>
    </div>
</template>

<script>
export default {
    name: "SavedRecipeItem",
    props: ["savedRecipie"]
}
</script>

<style scoped>
    .saved-recipe-item {
        padding: 10px;
        background: #f4f4f4;
        text-align: left;
        border-top: 1px #ccc dotted;
        border-bottom-right-radius: 10px;
        border-bottom-left-radius: 10px;
    }
    .del {
        background: #E07A5F;
        color: #fff;
        border: none;
        border-radius: 5px;
        float: right;
  }
  .view {
        background: #00a896;
        color: #fff;
        border: none;
        border-radius: 5px;
        float: right;
        margin-right: 8px !important;
  }
</style>