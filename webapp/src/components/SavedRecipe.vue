<template>
    <div class="savedRecipes">
        <h1>Saved</h1>
        <SavedRecipeContent 
            v-bind:toViewRecipe="toViewRecipe"
        />
        <div v-bind:key="savedRecipie.recipeID" v-for="savedRecipie in savedRecipies">
            <SavedRecipeItem 
                v-bind:savedRecipie="savedRecipie" 
                v-on:del-recipe="$emit('del-recipe', savedRecipie.recipeID)" 
                v-on:view-recipe="$emit('view-recipe', savedRecipie.recipeID)"
            />
        </div>
    </div>
</template>

<script>
import SavedRecipeItem from './SavedRecipeItem.vue';
import SavedRecipeContent from './SavedRecipeContent.vue';

export default {
    name: "SavedRecipes",
    data() {
        return {

        };
    },
    methods: {

    },
    created() {

    },
    components: {
        SavedRecipeItem,
        SavedRecipeContent
    },
    props: ["savedRecipies", "toViewRecipe"],
}
</script>

<style scoped>
.savedRecipes {
        border: 2px solid;
        border-radius: 10px;
    }
</style>