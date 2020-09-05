<template>
    <div class="ingredient-item">
        <p>
            {{ingredient.name}}
            <button @click="$emit('del-ingredient', ingredient.name)" class="del"> delete </button>
        </p>
    </div>
</template>

<script>
export default {
    name: "IngredientItem",
    props: ["ingredient"]
}
</script>

<style scoped>
    .ingredient-item {
        padding: 10px;
        background: #f4f4f4;
        text-align: left;
        border-top: 1px #ccc dotted;
    }
    .del {
        background: #E07A5F;
        color: #fff;
        border: none;
        border-radius: 5px;
        float: right;
  }
</style>