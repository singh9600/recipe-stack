<template>
    <div class="ingredients">
        <h1>Ingredients</h1>
        <div v-bind:key="ingredient.name" v-for="ingredient in ingredients">
            <IngredientItem v-bind:ingredient="ingredient" v-on:del-ingredient="$emit('del-ingredient', ingredient.name)" />
        </div>
        <form @submit="addIngredient">
            <input type="text" class="ingredient-input" v-model="name" name="name" placeholder="Add Ingredient">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
import IngredientItem from './IngredientItem.vue';

export default {
    name: "Ingredients",
    data() {
        return {
            name: ''
        }
    },
    methods: {
        addIngredient(e) {
            e.preventDefault();
            const newIngredient = {
                name: this.name
            }
            this.$emit('add-ingredient', newIngredient);
            this.name = '';
        }
    },
    created() {
        console.log(this.ingredients);
    },
    components: {
        IngredientItem
    },
    props: ["ingredients"]
}
</script>

<style scoped>
    .ingredients {
        border: 2px solid;
        border-radius: 10px;
    }
    .ingredient-input {
        padding: 10px;
        padding-bottom: 14px;
        background: #f4f4f4;
        text-align: left;
        border-style: none;
        border-top: 1px #ccc dotted;
        border-bottom-left-radius: 10px;
        width: 70%;
    }
    .ingredient-input:focus {
        outline: none;
    }
    .btn {
        background: #555;
        color: #fff;
        border-radius: 0px;
        border-bottom-right-radius: 6px;
        padding-top: 12px;
        padding-bottom: 12px;
        padding-left: 16px;
        width: 30%;
    }
</style>