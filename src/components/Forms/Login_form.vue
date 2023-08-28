<template>
  <div id="login_form">
    <navbar />
    <div id="form-view">
      <div class="form-container">
        <div class="form-heading">
          <h3 id="form-heading">Login form</h3>
        </div>
        <form name="login-form" autocomplete="off" id="form-body">
          <div class="form-item">
            <label for="username">Username: </label>
            <input id="username" class="input-text-field" type="text" name="username" required autocomplete="off"
              placeholder="Enter your username" v-model="user.name">
          </div>
          <div class="form-item">
            <label for="password">Password: </label>
            <input type="password" id="password" class="input-text-field" name="password" required autocomplete="off"
              placeholder="Enter your account password" v-model="user.password">
          </div>
          <div class="form-route-container form-item">
            <router-link class="form-route" to="/userregistrationform">Not registered? Register here</router-link>
            <span class="animated-line"></span>
          </div>
          <div class="form-item button-container">
            <button class="form-submit-button button" @click.prevent="loginuser">Login</button>
            <button class="form-reset-button button">Cancel</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import '../../assets/form_style.css'
import axios from 'axios';
import navbar from '../Navigationbar.vue'

export default {
  components: {
    navbar,
  },
  data() {
    return {
      user: {
        name: "",
        password: "",
      },
      errors: [],
      baseURL: "http://127.0.0.1:8000/api"
    }
  },
  methods: {
    async loginuser(){
      try{
        localStorage.setItem("token", (await axios.post(this.baseURL + '/userLogin', this.user)).data.token);
        
      } catch (error){
        this.errors.push(error);
        console.log(this.errors[this.errors.length]);
      }

      window.location.reload();
    }
  }
}
</script>

<style scoped>
</style>