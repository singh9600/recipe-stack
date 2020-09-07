<template>
  <div class="home">
    <div class="homeTop">
      <h1>RecipeSt<i class="fas fa-ice-cream"></i>ck</h1>
      <div class="steps">
        <!-- <p>1) Login or Create a new account.</p>
        <p>2) View countless randomly generated recipies.</p>
        <p>3) Save the ones you like for later.</p> -->
        <p>View countless randomly generated recipies based on the ingredients you have. Save the ones you like for later.</p>
        <p><i class="fas fa-robot"></i>  More features coming soon!  <i class="fas fa-robot"></i></p>
      </div>
      <router-link to="/login">
        <input class="btn btn-primary btn-lg" type="submit" value="Login">
      </router-link>
      <router-link to="/signup">
        <input class="btn btn-primary btn-lg" type="submit" value="SignUp">
      </router-link>
    </div>
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
    text-align: center;
    color: #3D405B;
    font-family: 'Ubuntu';
    display: grid;
    height: 100vh;
    grid-template-columns: 40px 50px auto 50px 40px;
    grid-template-rows: 25% auto 20px;
  }
  .homeTop {
    grid-column-start: 2;
    grid-column-end: 5;
    grid-row-start: 2;
    grid-row-end: 2;
  }
  .steps {
    padding-top: 20px;
    padding-bottom: 10px;
    padding-left: 500px;
    padding-right: 500px;
  }
  .btn {
    margin: 8px !important;
  }
  .fa-ice-cream {
    font-size: 70%;
  }
  @media screen and (max-width: 1700px) {
    .steps {
      padding-left: 400px;
      padding-right: 400px;
    }
  }
  @media screen and (max-width: 1180px) {
    .steps {
      padding-left: 0px;
      padding-right: 0px;
    }
  }
  @media screen and (max-width: 460px) {
    .home {
      grid-template-rows: 15% auto 20px;
    }
  }
</style>
