<template>
  <div>
    <h1>login Here</h1>
    <p>Username</p>
    <input type="text" v-model="username" />
    <p>Password</p>
    <input type="password" v-model="password" />
    <h3 @click="Login">Login</h3>
    <h4>{{ status }}</h4>
  </div>
</template>

<script>
import axios from "axios";
import cookies from "vue-cookies";
export default {
  name: "login-page",
  data() {
    return {
      username: "",
      password: "",
      status: ""
    };
  },
  methods: {
      Login: function() {
        this.status = "loading";
        axios
          .request({
            url: "https://reqres.in/api/login",
            method: "POST",
            headers: {
              "Content-Type": "application/json"
            },
            data: {
              email: this.username,
              password: this.password
            }
          })
          .then(response => {
            console.log(response);
            cookies.set('loginToken',response.data.token);
            console.log(response.data.token);
            this.status = "Successfully loggedin";
            this.$router.push({ name: 'Game' });

          })
          .catch(error => {
            console.log(error);
            this.status = "Invalid Login";

          });
      }
    }
};
</script>

<style scoped>
</style>