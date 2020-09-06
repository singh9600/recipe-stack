<template>
  <div class="recipes">
    <h1>Recipe</h1>
    <RecipeItem v-bind:generatedRecipe="generatedRecipe"/>
    <form @submit="generateRecipe">
        <input type="submit" value="Save Recipe" class="btn">
        <input type="submit" value="New Recipe" class="btn">
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
        width: 30%;
        margin: 8px !important;
    }
</style>
