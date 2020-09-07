<template>
  <div class="profile">
    <div class="val ingredients">
      <Ingredients
        v-bind:ingredients="ingredients"
        v-on:del-ingredient="deleteIngredient"
        v-on:add-ingredient="addIngredient"
      />
    </div>
    <div class="val recipies">
      <Recipes
        v-bind:generatedRecipe="generatedRecipe"
        v-on:generate-recipe="generateRecipe"
        v-on:save-recipe="saveRecipe"
      />
    </div>
    <div class="val savedRecipies">
      <SavedRecipe
        v-bind:savedRecipies="savedRecipies"
        v-bind:toViewRecipe="toViewRecipe"
        v-on:del-recipe="deleteRecipe"
        v-on:view-recipe="viewRecipe"
      />
    </div>
  </div>
</template>

<script>
import Recipes from "@/components/Recipes.vue";
import SavedRecipe from "@/components/SavedRecipe.vue";
import Ingredients from "@/components/Ingredients.vue";
import qs from "qs";
import axios from "axios";

export default {
  name: "Profile",
  components: {
    Recipes,
    SavedRecipe,
    Ingredients,
  },
  data() {
    return {
      recipes: [],
      generatedRecipe: "",
      ingredients: [],
      savedRecipies: [],
      toViewRecipe: "",
    };
  },
  methods: {
    // gets all the ingredients from the user's database
    getIngredients() {
      var token = localStorage.getItem("token");
      var data = qs.stringify({
        username: this.$route.query.username,
      });
      var config = {
        method: "post",
        url: "https://guarded-eyrie-04910.herokuapp.com/getIngredients",
        headers: {
          Authorization: `Bearer ${token}`,
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };

      let self = this;
      axios(config)
        .then(function(response) {
          console.log(JSON.stringify(response.data));
          self.ingredients = response.data;
          console.log(JSON.stringify(self.ingredients));
        })
        .catch(function(error) {
          console.log(error);
        });
    },

    // delets the particular ingredient from the user's database
    deleteIngredient(name) {
      var token = localStorage.getItem("token");
      var data = qs.stringify({
        username: this.$route.query.username,
        ingredientName: name,
      });
      var config = {
        method: "delete",
        url: "https://guarded-eyrie-04910.herokuapp.com/ingredients/",
        headers: {
          Authorization: `Bearer ${token}`,
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

      this.ingredients = this.ingredients.filter(
        (ingredient) => ingredient.name !== name
      );
    },

    // adds the particular ingredient to the user's database
    addIngredient(newIngredient) {
      if (newIngredient.name) {
        var token = localStorage.getItem("token");
        var data = qs.stringify({
          username: this.$route.query.username,
          name: newIngredient.name,
        });
        var config = {
          method: "post",
          url: "https://guarded-eyrie-04910.herokuapp.com/ingredients",
          headers: {
            Authorization: `Bearer ${token}`,
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

        this.ingredients = [...this.ingredients, newIngredient];
      }
    },

    // generates recipe from spoonacular
    generateRecipe() {
      let ingredientStr = "";
      this.ingredients.forEach((element) => {
        ingredientStr = ingredientStr + element.name + ",+";
        // console.log(element.name);
      });
      ingredientStr = ingredientStr.slice(0, -2);
      console.log(ingredientStr);

      var data = qs.stringify({
        ingredientStr: ingredientStr,
      });
      var config = {
        method: "post",
        url: "https://guarded-eyrie-04910.herokuapp.com/spoonacularRecipe",
        headers: {
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };

      let self = this;
      axios(config)
        .then(function(response) {
          console.log(JSON.stringify(response.data));
          self.generatedRecipe = response.data;
        })
        .catch(function(error) {
          console.log(error);
        });
    },

    // save a recipe to the user database
    saveRecipe(selectedRecipe) {
      var data = qs.stringify({
        username: this.$route.query.username,
        title: selectedRecipe.title,
        id: selectedRecipe.recipeID,
      });
      var token = localStorage.getItem("token");
      var config = {
        method: "post",
        url: "https://guarded-eyrie-04910.herokuapp.com/recipes",
        headers: {
          Authorization: `Bearer ${token}`,
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };
      let self = this;
      axios(config)
        .then(function(response) {
          console.log(JSON.stringify(response.data));
          self.savedRecipies = [...self.savedRecipies, selectedRecipe];
          console.log(selectedRecipe);
          console.log(self.savedRecipies);
        })
        .catch(function(error) {
          console.log(error);
        });
    },

    // returns all saved recipes
    getSavedRecipies() {
      var data = qs.stringify({
        username: this.$route.query.username,
      });
      var token = localStorage.getItem("token");
      var config = {
        method: "post",
        url: "https://guarded-eyrie-04910.herokuapp.com/getrecipes",
        headers: {
          Authorization: `Bearer ${token}`,
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };
      let self = this;
      axios(config)
        .then(function(response) {
          self.savedRecipies = response.data;
        })
        .catch(function(error) {
          console.log(error);
        });
    },

    // delete a recipe from user's database
    deleteRecipe(recipeID) {
      var data = qs.stringify({
        username: this.$route.query.username,
        id: recipeID,
      });
      var token = localStorage.getItem("token");
      var config = {
        method: "delete",
        url: "https://guarded-eyrie-04910.herokuapp.com/recipes",
        headers: {
          Authorization: `Bearer ${token}`,
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };
      let self = this;
      axios(config)
        .then(function(response) {
          console.log(JSON.stringify(response.data));
          self.savedRecipies = self.savedRecipies.filter(
            (recipe) => recipe.recipeID !== recipeID
          );
        })
        .catch(function(error) {
          console.log(error);
        });
    },

    // views the selected recipe in the SavedRecipeContent component
    viewRecipe(recipeID) {
      var data = qs.stringify({});
      var config = {
        method: "post",
        url: `https://guarded-eyrie-04910.herokuapp.com/spoonacularRecipe/${recipeID}`,
        headers: {},
        data: data,
      };
      let self = this;
      axios(config)
        .then(function(response) {
          self.toViewRecipe = response.data;
          console.log(JSON.stringify(response.data));
        })
        .catch(function(error) {
          console.log(error);
        });
    },
  },
  created() {
    console.log("started");
    this.getIngredients();
    this.getSavedRecipies();
    console.log(JSON.stringify(this.ingredients));
  },
};
</script>

<style scoped>
.profile {
  text-align: center;
  color: #3d405b;
  font-family: "Ubuntu";
  display: grid;
  height: 100vh;
  grid-template-columns: auto 25px 28% 25px 28% 25px 28% 25px auto;
  grid-template-rows: 5% auto 20px;
}
.ingredients {
  grid-column-start: 3;
  grid-column-end: 3;
  grid-row-start: 2;
  grid-row-end: 2;
}
.recipies {
  grid-column-start: 5;
  grid-column-end: 5;
  grid-row-start: 2;
  grid-row-end: 2;
}
.savedRecipies {
  grid-column-start: 7;
  grid-column-end: 7;
  grid-row-start: 2;
  grid-row-end: 2;
}
@media screen and (max-width: 740px) {
  .profile {
    display: inline;
  }
}
</style>
