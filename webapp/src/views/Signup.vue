<template>
  <div class="signup">
    <form @submit="Signup" class="signup-form">
      <div class="heading">SignUp</div>
      <div class="username">
        <input type="username" v-model="username" class="form-control" placeholder="username" />
      </div>
      <div class="password">
        <input type="password" v-model="password" class="form-control" placeholder="password" />
      </div>
      <div class="signupBtn">
        <input class="btn btn-primary" type="submit" value="SignUp" />
        <router-link to="/">
          <input class="btn btn-primary" type="submit" value="Cancel" />
        </router-link>
      </div>
    </form>
  </div>
</template>

<script>
import qs from "qs";
import axios from "axios";
import md5 from "md5";

export default {
  name: "signup",
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    Signup(e) {
      e.preventDefault();
      var data = qs.stringify({
        username: this.username,
        password: md5(this.password),
      });
      var config = {
        method: "post",
        url: "https://guarded-eyrie-04910.herokuapp.com/user/signup",
        headers: {
          "Content-Type": "application/x-www-form-urlencoded",
        },
        data: data,
      };

      let self = this;
      axios(config)
        .then(function(response) {
          console.log(JSON.stringify(response.data));
          self.$router.push({
            name: "Login",
          });
        })
        .catch(function(error) {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped>
.signup {
  text-align: center;
  color: #3d405b;
  font-family: "Ubuntu";
  display: grid;
  height: 100vh;
  justify-content: center;
  grid-template-columns: 40px 50px auto 50px 40px;
  grid-template-rows: 25% 300px auto;
}
.signup-form {
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
.signupBtn {
  padding-bottom: 10px;
}
</style>
