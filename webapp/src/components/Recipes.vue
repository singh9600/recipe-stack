<template>
  <div>
    <h1>Recipe</h1>
  </div>
</template>

<script>
import qs from "qs";
import axios from "axios";

export default {
  name: "Recipes",
  data() {
    return {
      ingredientStr: ""
    };
  },
  methods: {
    generateRecipe(ingredientStr) {
      var data = qs.stringify({
        ingredientStr: ingredientStr,
      });
      var config = {
        method: "post",
        url: "http://localhost:3000/spoonacularRecipe",
        headers: {
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };

      axios(config)
        .then(function(response) {
          console.log(JSON.stringify(response.data));
        })
        .catch(function(error) {
          console.log(error);
        });
    },

    generateIngredientString() {
        this.ingredientStr = "";
        this.ingredients.forEach(element => {
            this.ingredientStr = this.ingredientStr + element.name + ',+';
            // console.log(element.name);
        });
        this.ingredientStr = this.ingredientStr.slice(0, -2);
        console.log(this.ingredientStr);
        this.generateRecipe(this.ingredientStr);
    }
  },
  created() {
      console.log(JSON.stringify(this.ingredients));
      this.generateIngredientString();
  },
  props: ["ingredients"],
};
</script>

<style scoped>

</style>
