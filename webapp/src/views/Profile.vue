<template>
    <div class="profile">
        <div class="val ingredients">
            <h1>Ingredients</h1>
        </div>
        <div class="val recipies">
            <h1>Recipies</h1>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Profile',
    components: {

    },
    data() {
        return {
            recipies: []
        }
    },
    created() {
    }
}
</script>

<style scoped>
    .profile {
        text-align: center;
        color: #427286;
        font-family: 'Ubuntu';
        display: grid;
        height: 100vh;
        grid-template-columns: 33% 33% 33% auto;
        grid-template-rows: 5% auto 20px;
    }
    .ingredients {
        grid-column-start: 1;
        grid-column-end: 1;
        grid-row-start: 2;
        grid-row-end: 2;
    }
    .recipies {
        grid-column-start: 2;
        grid-column-end: 2;
        grid-row-start: 2;
        grid-row-end: 2;
    }
    @media screen and (max-width: 740px) {
    .profile {
      display: inline;
    }
  }
</style>