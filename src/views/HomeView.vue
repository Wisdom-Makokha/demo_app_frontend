<script >
import axios from 'axios'

export default {
  data() {
    return {
      user: {
        name: "",
        email: "",
        password: "",
        townid: null
      },
      towns: [],
      errors: [],
      baseUrl: "http://127.0.0.1:8000/api",
      
    }
  },
  mounted() {
    axios
      .get(this.baseUrl + '/readAllTowns')
      .then(response => (this.towns = response.data))
      .catch(error => this.errors = error)
  },
  methods:{
    formdataprocessing(){
      console.log(this.user);
      axios
      .post(this.baseUrl + '/createUser', this.user)
      .then(response => (console.log(response)))
      .catch(error => this.errors = error);
      console.log(this.errors);
    }
  }
}
</script>

<template>
  <div id="homeview">
    <div class="form-container">
      <div class="form-heading">
        <h2 id="form-heading">User registration form</h2>
      </div>
      <form name="user-registration" autocomplete="off" >
        <div class="form-item">
          <label for="username">Name: </label>
          <input type="text" v-model="user.name" id="username" name="username" class="input-text-field" required placeholder="Enter your full name">
        </div>
        <div class="form-item">
          <label for="email">Email: </label>
          <input type="email" id="email" v-model="user.email" name="email" class="input-text-field" required placeholder="johndoe@example.com">
        </div>
        <div class="form-item">
          <label for="town-selection">Towns: </label>
          <select v-model="user.townid" name="town-selection" id="town-selection" class="input-text-field" placeholder="Pick a town">
            <option disabled value="">Please select an option</option>
            <option v-for="town in towns" :key="town.id" :value="town.id">
              {{ town.name }}
            </option>
          </select>
        </div>
        <div class="form-item">
          <label for="password">Password: </label>
          <input type="password" v-model="user.password" id="password" name="password" class="input-text-field" required placeholder="Enter your password">
        </div>
        <div class="form-item">
          <button type="submit" @click.prevent="formdataprocessing">Submit</button>
        </div>
      </form>
    </div>
  </div>
</template>


<style scoped>
#homeview {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.form-container {
  background-color: rgb(222, 222, 222);
  height: fit-content;
  width: fit-content;
  padding-left: 80px;
  padding-right: 80px;
  padding-top: 60px;
  padding-bottom: 60px;
  border: 3px solid rgb(157, 157, 157);
  border-radius: 20px;
  box-shadow: 3px 5px 10px rgba(0, 0, 0, 0.4)
}

.user-registration {
  display: flex;
  flex-direction: column;
  align-items: start;
}

.form-item{
  margin: 20px;
  display: flex;
  flex-direction: column;
  align-items: start;
}

.input-text-field{
  font-size: 110%;
  height: 30px;
  min-width: 340px;
  border-radius: 6px;
  border: 2px solid rgb(112, 112, 112);
}

.input-text-field:focus, .input-text-field:hover, input-text-field:checked{
  border-color: rgb(58, 147, 243);
}

.form-heading{
  text-align: center
}
</style>