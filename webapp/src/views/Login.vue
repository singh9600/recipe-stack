<template>
  <div class="login">
    <form @submit="Login" class="login-form">
      <div class="heading">Login</div>
      <div class="username">
        <input
          type="username"
          v-model="username"
          class="form-control"
          placeholder="username"
        />
      </div>
      <div class="password">
        <input
          type="password"
          v-model="password"
          class="form-control"
          placeholder="password"
        />
      </div>
      <div>
        {{passCheck}}
      </div>
      <div class="loginBtn">
        <input class="btn btn-primary" type="submit" value="Login" />
        <router-link to="/">
          <input class="btn btn-primary cancel" value="Cancel" />
        </router-link>
      </div>
      <p class="message">
        Not registered?
        <router-link to="/signup">Create an account</router-link>
      </p>
    </form>
  </div>
</template>

<script>
import qs from "qs";
import axios from "axios";
import md5 from "md5";

export default {
  name: "login",
  data() {
    return {
      username: "",
      password: "",
      passCheck: "",
      token: "",
    };
  },
  mounted() {
    if (localStorage.token) {
      this.token = localStorage.token;
    }
  },
  watch: {
    name(newToken) {
      localStorage.token = newToken;
    }
  },
  methods: {
    Login(e) {
      e.preventDefault();
      var data = qs.stringify({
        username: this.username,
        password: md5(this.password),
      });
      var config = {
        method: "post",
        url: "https://guarded-eyrie-04910.herokuapp.com/user/login",
        headers: {
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };
      let self = this;
      axios(config)
        .then(function(response) {
          let resVal = JSON.stringify(response.data);
          if(resVal.localeCompare("\"Wrong username or password\"") === 0) {
            self.passCheck = "Wrong Username or Password";
          }
          else{
            localStorage.token = response.data.token;
            self.$router.push({
              name: "Profile",
              query: {
                username: self.username,
            }});
          }
        })
        .catch(function(error) {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped>
.login {
  text-align: center;
  color: #3d405b;
  font-family: "Ubuntu";
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
.cancel {
  width: 80px;
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
