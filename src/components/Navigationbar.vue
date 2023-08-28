<template>
    <div id="navigationbar">
        <div class="navigation-container">
            <div class="home-container route-container">
                <router-link to="/" class="home route">Home</router-link>
            </div>
            <div class="other-routes">
                <div class="route-container" v-if="checklogin">
                    <router-link to="/userstable" class="route" title="users table">Users</router-link>
                </div>
                <div class="dropdown-menu route-container">
                    <input type="checkbox" id="dropdown">
                    <label for="dropdown" class="dropdown-button">
                        <span class="route">More options</span>
                        <span class="arrow"></span>
                    </label>
                    <div class="dropdown-container">
                        <div class="dropdown-route-container register-container">
                            <router-link to="/userregistrationform" class="dropdown-route register">Register</router-link>
                        </div>
                        <div class="dropdown-route-container">
                            <router-link to="/login" class="dropdown-route">Login</router-link>
                        </div>

                        <div class="dropdown-route-container">
                            <a class="dropdown-route" @click="logoutuser">Logout</a>
                        </div>
                    </div>
                </div>
                <div class="route-container about-container">
                    <router-link to="/about" class="route about">About</router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped></style>

<script>
import axios from 'axios';
import '../assets/navigationbarstyle.css'

export default {
    data() {
        return {
            baseURL: "http://127.0.0.1:8000/api",
            errors: [],
            checklogin: localStorage.getItem("token") ? true : false,
        }
    },
    methods: {
        logoutuser() {
            axios.post(this.baseURL + '/userLogout')
                .then(response => console.log(response.data.message))
                .catch(error => (this.errors.push(error)));

            localStorage.removeItem("token");
            window.location.reload();
        }
    }
}
</script>