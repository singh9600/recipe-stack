<template>
    <div class="login">
        <form class="login-form">
            <div class="heading">Login</div>
            <div class="username"><input type="username" class="form-control" placeholder="username"></div>
            <div class="password"><input type="password" class="form-control" placeholder="password"></div>
            <div class="loginBtn">
                <input class="btn btn-primary" type="submit" value="Login">
                <router-link to="/">
                    <input class="btn btn-primary" type="submit" value="Cancel">
                </router-link>
            </div>
            <p class="message">Not registered? <router-link to="/signup">Create an account</router-link></p>
        </form>
     </div>
</template>

<script>
export default {};
</script>

<style scoped>
  .login {
    text-align: center;
    color: #3D405B;
    font-family: 'Ubuntu';
    display: grid;
    height: 100vh;
    justify-content: center;
    grid-template-columns: 40px 50px auto 50px 40px;
    grid-template-rows: 25% 300px auto;
  }
  .login-form {
    grid-column-start: 3;
    grid-column-end: 3;
    grid-row-start: 2;
    grid-row-end: 2;
    align-self: center;
    width: 300px;
    padding: 10px;
    border-style: solid;
    border-radius: 5px;
  }
  .btn {
    margin: 8px !important;
  }
  .heading {
      font-weight: 500;
      font-size: 30px;
      padding-bottom: 10px;
  }
  .username {
      padding-bottom: 10px;
  }
  .password {
      padding-bottom: 10px;
  }
  .loginBtn {
      padding-bottom: 10px;
  }
</style>
