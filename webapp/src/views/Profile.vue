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
      <Recipes v-bind:ingredients="ingredients" />
    </div>
  </div>
</template>

<script>
import Recipes from "@/components/Recipes.vue";
import Ingredients from "@/components/Ingredients.vue";
import qs from "qs";
import axios from "axios";

export default {
  name: "Profile",
  components: {
    Recipes,
    Ingredients,
  },
  data() {
    return {
      recipes: [],
      ingredients: [],
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
        url: "http://localhost:3000/getIngredients",
        headers: {
          Authorization: `Bearer ${token}`,
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };

      let self = this;
      axios(config)
        .then(function (response) {
          //console.log(response.data);
          self.ingredients = response.data;
        })
        .catch(function (error) {
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
        url: "http://localhost:3000/ingredients/",
        headers: {
          Authorization: `Bearer ${token}`,
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };

      axios(config)
        .then(function (response) {
          console.log(JSON.stringify(response.data));
        })
        .catch(function (error) {
          console.log(error);
        });

      this.ingredients = this.ingredients.filter(
        (ingredient) => ingredient.name !== name
      );
    },

    // adds the particular ingredient to the user's database
    addIngredient(newIngredient) {
      var token = localStorage.getItem("token");
      var data = qs.stringify({
        username: this.$route.query.username,
        name: newIngredient.name,
      });
      var config = {
        method: "post",
        url: "http://localhost:3000/ingredients",
        headers: {
          Authorization: `Bearer ${token}`,
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };

      axios(config)
        .then(function (response) {
          console.log(JSON.stringify(response.data));
        })
        .catch(function (error) {
          console.log(error);
        });

      this.ingredients = [...this.ingredients, newIngredient];
    },
  },
  created() {
    console.log("started");
    this.getIngredients();
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
  grid-template-columns: 25px 33% 33% 33% 25px;
  grid-template-rows: 5% auto 20px;
}
.ingredients {
  grid-column-start: 2;
  grid-column-end: 2;
  grid-row-start: 2;
  grid-row-end: 2;
}
.recipies {
  grid-column-start: 3;
  grid-column-end: 3;
  grid-row-start: 2;
  grid-row-end: 2;
}
@media screen and (max-width: 740px) {
  .profile {
    display: inline;
  }
}
</style>
