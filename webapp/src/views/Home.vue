<template>
  <div class="home">
    <h1>RecipeSt<i class="fas fa-ice-cream"></i>ck</h1>
    <p>Generate countless recipies and save the ones you like for later.</p>
    <div class="inputs">
      <input class="btn btn-primary" type="submit" value="Login">
      <input class="btn btn-primary" type="submit" value="SignUp">
    </div>
    <img 
      src="@/assets/MIXING BOWL 1.svg"
      class="homeImg">
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    
  }
}
</script>

<style scoped>
  h1 {
    font-size: 300%;
  }
  p {
    font-size: 150%;
  }
  .home {
    padding-top: 15%;
    text-align: center;
    color: #427286;
    font-family: 'Ubuntu';
  }
  .btn {
    margin: 8px !important;
  }
  .fas {
    font-size: 70%;
  }
</style>
