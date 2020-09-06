<template>
    <div class="profile">
        <div class="val ingredients">
            <Ingredients v-bind:ingredients="ingredients" v-on:del-ingredient="deleteIngredient" v-on:add-ingredient="addIngredient" />
        </div>
        <div class="val recipies">
            <Recipes v-bind:ingredients="ingredients" />
        </div>
    </div>
</template>

<script>
import Recipes from '@/components/Recipes.vue';
import Ingredients from '@/components/Ingredients.vue';

export default {
    name: 'Profile',
    components: {
        Recipes,
        Ingredients
    },
    data() {
        return {
            recipes: [
                {
                    username: "user1",
                    recipeID: "792587"
                },
                {
                    username: "user1",
                    recipeID: "638816"
                },
                {
                    username: "user1",
                    recipeID: "635063"
                }
            ],
            ingredients: [
                {
                    username: "user1",
                    name: "Sugar"
                },
                {
                    username: "user1",
                    name: "Apple"
                },
                {
                    username: "user1",
                    name: "Tomato"
                }
            ]
        }
    },
    methods: {
        deleteIngredient(name) {
            this.ingredients = this.ingredients.filter(ingredient => ingredient.name !== name);
        },
        addIngredient(newIngredient) {
            this.ingredients = [...this.ingredients, newIngredient];
        }
    },
    created() {
    }
}
</script>

<style scoped>
    .profile {
        text-align: center;
        color: #3D405B;
        font-family: 'Ubuntu';
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