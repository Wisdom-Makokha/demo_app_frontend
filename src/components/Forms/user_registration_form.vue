<script >
import '../../assets/form_style.css'
import axios from 'axios'
import navbar from '../Navigationbar.vue'

export default {
  components: {
    navbar,
  },
  data() {
    return {
      user: {
        name: "",
        email: "",
        password: "",
        password_confirmation: "",
        townid: null
      },
      name: "",
      email: "",
      towns: [],
      errors: [],
      baseUrl: "http://127.0.0.1:8000/api",
    }
  },
  mounted() {
    axios
      .get(this.baseUrl + '/readAllTowns')
      .then(response => (this.towns = response.data.requestdata))
      .catch(error => this.errors.push(error))
  },
  methods: {
    formdataprocessing() {
      axios
        .post(this.baseUrl + '/createUser', this.user)
        .then(response => (console.log(response.data.token)))
        .catch(error => this.errors = error);
      console.log(this.errors);

      formreset;
    },
    formreset() {
      this.user.name = "";
      this.user.email = "";
      this.user.password = "";
      this.user.townid = null;
    }
  }
}
</script>

<template>
  <div id="formpage">
    <navbar />
    <div id="form-view">
      <div class="form-container">
        <div class="form-heading">
          <h2 id="form-heading">User registration form</h2>
        </div>
        <form name="user-registration" autocomplete="off" id="form-body">
          <div class="form-item">
            <label for="username">Name: </label>
            <input type="text" v-model="user.name" id="username" name="username" class="input-text-field" required
              placeholder="Enter your full name">
          </div>
          <div class="form-item">
            <label for="email">Email: </label>
            <input type="email" id="email" v-model="user.email" name="email" class="input-text-field" required
              placeholder="johndoe@example.com">
          </div>
          <div class="form-item">
            <label for="town-selection">Towns: </label>
            <select v-model="user.townid" name="town-selection" id="town-selection" class="input-text-field"
              placeholder="Pick a town">
              <option disabled value="">Please select an option</option>
              <option v-for="town in towns" :key="town.id" :value="town.id">
                {{ town.name }}
              </option>
            </select>
          </div>
          <div class="form-item">
            <label for="password">Password: </label>
            <input type="password" v-model="user.password" id="password" name="password" class="input-text-field" required
              placeholder="Enter your password">
          </div>
          <div class="form-item">
            <label for="confirm_password">Confirm password: </label>
            <input type="password" v-model="user.password_confirmation" id="confirm_password" name="confirm_password"
              class="input-text-field" required placeholder="Confirm your password">
          </div>
          <div class="form-route-container form-item">
            <router-link to="/login" class="form-route">Registered already? Login here</router-link>
            <span class="animated-line"></span>
          </div>
          <div class="button-container">
            <button type="submit" @click.prevent="formdataprocessing" class="form-submit-button button">Submit</button>
            <button @click.prevent="formreset" class="button form-reset-button">Reset</button>
          </div>
        </form>
      </div>
    </div>

  </div>
</template>


<style scoped>

</style>