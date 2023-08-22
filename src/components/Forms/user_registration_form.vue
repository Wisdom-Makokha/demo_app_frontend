<script >
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
      .then(response => (this.towns = response.data))
      .catch(error => this.errors.push(error))
  },
  methods: {
    formdataprocessing() {
      axios
        .post(this.baseUrl + '/createUser', this.user)
        .then(response => (console.log(response)))
        .catch(error => this.errors = error);
      console.log(this.errors);
      
      formreset();
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
    <div id="formview">
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
          <div class="button-container">
            <div class="form-item">
              <button type="submit" @click.prevent="formdataprocessing" class="form-submit-button button">Submit</button>
            </div>
            <div class="form-item">
              <button @click.prevent="formreset" class="button form-reset-button">Reset</button>
            </div>
          </div>
        </form>
      </div>
    </div>

  </div>
</template>


<style scoped>
#formview {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 60px;
}

#form-body {
  background-color: rgba(255, 255, 255, 0.8);
  padding-right: 50px;
  padding-left: 50px;
  padding-bottom: 45px;
  padding-top: 20px;
  border-radius: 20px
}

.form-container {
  background-color: rgb(222, 222, 222);
  height: fit-content;
  width: fit-content;
  padding-left: 15px;
  padding-right: 15px;
  padding-top: 20px;
  padding-bottom: 15px;
  border: 3px solid rgb(157, 157, 157);
  border-radius: 20px;
  box-shadow: 3px 5px 10px rgba(0, 0, 0, 0.4)
}

.user-registration {
  display: flex;
  flex-direction: column;
  align-items: start;
}

.form-item {
  margin: 20px;
  display: flex;
  flex-direction: column;
  align-items: start;
}

.input-text-field {
  font-size: 110%;
  height: 30px;
  min-width: 340px;
  border-radius: 6px;
  border: 2.5px solid rgb(112, 112, 112);
}

.input-text-field:focus-visible,
.input-text-field:hover,
input-text-field:checked {
  border-color: rgb(58, 147, 243);
  outline-color: rgb(58, 147, 243);
}

.form-heading {
  text-align: center
}

.button-container {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.button {
  padding: 12px;
  font-size: 110%;
  border: 3px solid rgb(97, 97, 97);
  border-radius: 14px;
  background-color: rgb(176, 176, 176);
  transition: background-color 0.7s, box-shadow 0.7s ease-in-out;
  box-shadow: 1.8px 2.5px 3.4px 0.5px rgba(0, 0, 0, 0.6);
  cursor: pointer
}

.form-submit-button:hover {
  color: white;
  background-color: rgb(86, 125, 205);
  box-shadow: 3.8px 2.5px 8.4px 0.5px rgba(86, 125, 205, 0.8)
}

.form-reset-button:hover {
  color: white;
  background-color: rgb(239, 63, 63);
  box-shadow: 3.8px 2.5px 8.4px 0.5px rgba(239, 63, 63, 0.8)
}
</style>