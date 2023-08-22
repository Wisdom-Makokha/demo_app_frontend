<template>
    <div id="navigationbar">
        <div class="navigation-container">
            <div class="home-container route-container">
                <router-link to="/" class="home route">Home</router-link>
            </div>
            <div class="other-routes">
                <div class="route-container more-routes">
                    <div>More</div>
                    <div class="dropdown-container">
                        <div class="dropdown-route">
                            <a>Link 1</a>
                        </div>
                        <div class="dropdown-route">
                            <a>Link 2</a>
                        </div>
                        <div class="dropdown-route">
                            <a>Link 3</a>
                        </div>
                    </div>
                </div>
                <div class="route-container about-container">
                    <router-link to="/about" class="route about">About</router-link>
                </div>
                <div class="route-container register-container">
                    <router-link to="/userregistrationform" class="route register">Register</router-link>
                </div>

            </div>
        </div>
    </div>
</template>

<style scoped>
#navigationbar{
    top: 0;
    
}

.navigation-container{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    height: fit-content;
    border-bottom: 2px solid rgba(79, 79, 79, 0.4);
    background-color: rgba(45, 45, 45, 0.4);
    position: sticky;
    box-shadow: 0px 4px 10px 1px rgba(0, 0, 0, 0.4)
}

.route-container{
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 18px;
    padding-bottom: 5px;
}

.route{
    text-decoration: none;
    font-size: 120%;
    color: black;
    transition: color 0.4s;
}

.route:hover, .route:focus{
    color: rgb(58, 147, 243)
}

.dropdown-container{
    background-color: rgba(45, 45, 45, 0.8);
    max-height: 0;
    overflow: hidden;
    position: absolute;
    box-sizing: border-box;
    transition: all 0.4s linear
}

.more-routes:hover >.dropdown-container{
    max-height: 100px;
    border: 2px solid rgba(79, 79, 79, 0.4);
    display: flex;
    flex-direction: column;
    justify-content: start;
    align-items: center;
}

.other-routes{
    display: flex;
    padding-right: 6.8%;
}

.home-container{
    padding-left: 8.8%;
}

.home{
    font-weight: 140%;
    font-size: 140%;
}

</style>

<script>

</script>