<template>
  <div class="recipes">
    <h1>Recipe</h1>
    <RecipeItem v-bind:generatedRecipe="generatedRecipe"/>
    <form>
        <input type="submit" v-on:click="saveRecipe" value="Save Recipe" class="btn">
        <input type="submit" v-on:click="generateRecipe" value="Generate Recipe" class="btn">
    </form>
  </div>
</template>

<script>
import RecipeItem from './RecipeItem.vue';

export default {
  name: "Recipes",
  data() {
    return {
      
    };
  },
  methods: {
      generateRecipe(e) {
          e.preventDefault();
          this.$emit('generate-recipe');
      },
      saveRecipe(e) {
        e.preventDefault();
        const selectedRecipe = {
          recipeID: this.generatedRecipe.id,
          title: this.generatedRecipe.title,
        }
        this.$emit('save-recipe', selectedRecipe);
      }
  },
  created() {
    
  },
  components: {
      RecipeItem
  },
  props: ["generatedRecipe"],
};
</script>

<style scoped>
.recipes {
        border: 2px solid;
        border-radius: 10px;
    }
.btn {
        background: #555;
        color: #fff;
        padding: 5px;
        width: 40%;
        white-space: normal;
        margin: 8px !important;
    }
</style>
