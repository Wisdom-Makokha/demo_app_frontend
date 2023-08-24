<template>
    <div id="navigationbar">
        <div class="navigation-container">
            <div class="home-container route-container">
                <router-link to="/" class="home route">Home</router-link>
            </div>
            <div class="other-routes">
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
                            <router-link to="/userstable" class="dropdown-route">Users</router-link>
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

<style scoped>
#navigationbar {
    top: 0;

}

.navigation-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    height: fit-content;
    border-bottom: 2px solid rgba(79, 79, 79, 0.4);
    background-color: rgba(34, 34, 34, 0.5);
    position: sticky;
    box-shadow: 0px 4px 10px 1px rgba(0, 0, 0, 0.4)
}

.route-container {
    min-width: 70px;
    height: 22px;
    padding-left: 15px;
    padding-right: 15px;
    padding-top: 18px;
    padding-bottom: 5px;
    margin: 3px;
    text-align: center;
    cursor: pointer;
}

.route {
    text-decoration: none;
    font-size: 120%;
    color: black;
    transition: color 0.4s;
}

.route:hover {
    color: white;
}

input[type="checkbox"]:checked + label >.route{
    color: white;
}

.dropdown-menu {
    position: relative;
}

input[type="checkbox"]{
    opacity: 0;
    position: absolute
}

.dropdown-button{
    display: flex;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
}

.dropdown-container {
    max-height: 0;
    min-width: 70px;
    max-width: fit-content;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    position: absolute;
    margin-top: 9px;
    left: inherit;
    border: 0px solid transparent;
    transition-property: max-height, border;
    transition-duration: 0.2s;
    transition-timing-function: linear;
    background-color: rgb(66, 66, 66)
}

.arrow{
    border-left: 5px solid transparent;
    border-right: 5px solid transparent;
    border-top: 6px solid black;
    transition: border-top ease-in-out 0.6s, transform ease-in-out 0.6s;
}

input[type="checkbox"]:hover + label >.arrow{
    transform: rotate(180deg);
    border-top-color: white;
}

input[type="checkbox"]:checked + label >.arrow{
    transform: rotate(180deg);
    border-top-color: white;
}

.dropdown-menu:hover >.dropdown-container{
    max-height: 100px;
    border: 1px solid rgb(66, 66, 66);
}

.dropdown-menu:hover >.dropdown-button >.arrow{
    transform: rotate(180deg);
    border-top-color: white;
}

.dropdown-menu:hover >.dropdown-button >.route{
    color: white;
}

input[type="checkbox"]:checked ~.dropdown-container{
    max-height: 100px;
    border: 1px solid rgb(66, 66, 66);
}

.dropdown-route-container{
    padding-left: 15px;
    padding-right: 15px;
    padding-top: 7px;
    padding-bottom: 4px;
    text-align: center;
    border-bottom: 2px solid rgb(40, 40, 40);
    background-color: rgba(143, 143, 143, 0.8);
}

.dropdown-route-container:hover{
    background-color: rgba(176, 176, 176, 0.9);
}

.dropdown-route {
    text-decoration: none;
    font-size: 120%;
    color: black;
    transition: color 0.4s;
}

.dropdown-route:hover{
    color: white;
}

.other-routes {
    display: flex;
    margin-right: 6.8%;
}

.home-container {
    margin-left: 8.8%;
}

.home {
    font-weight: 140%;
    font-size: 140%;
}
</style>

<script>

</script>