<template>
    <div id="usertable">
        <navbar />
        <div class="table-position">
            <div class="table-container">
                <div class="table-title">
                    <h2 id="table-heading">User table</h2>
                </div>
                <div class="table-header">
                    <div class="username-header header-cell cell username-column">
                        <h3 class="username-header-text">Username</h3>
                    </div>
                    <div class="email-header header-cell cell email-column">
                        <h3 class="email-header-text">Email</h3>
                    </div>
                    <div class="phonenumber-header header-cell cell phonenumber-column">
                        <h3 class="phonenumber-header-text">Phone number</h3>
                    </div>
                    <div class="town-header header-cell cell town-column">
                        <h3 class="town-header-text">Town</h3>
                    </div>
                    <div class="actions-header header-cell cell actions-column">
                        <h3 class="actions-header-text">Actions</h3>
                    </div>
                </div>
                <div class="table-body" v-for="user in users" :key="user.id">
                    <div class="username-record body-cell cell username-column">
                        <p class="username-text">{{ user.username }}</p>
                    </div>
                    <div class="email-record body-cell cell email-column">
                        <p class="email-text">{{ user.email }}</p>
                    </div>
                    <div class="phonenumber-record body-cell cell phonenumber-column">
                        <p class="phonenumber-text">{{ user.phonenumber }}</p>
                    </div>
                    <div class="town-record body-cell cell town-column">
                        <p class="town-text">{{ user.town }}</p>
                    </div>
                    <div class="action-record body-cell cell actions-column">
                        <button class="table-button update-button">Update</button>
                        <button @click="deleteuser(user.id)" class="table-button delete-button">Delete</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import navbar from '../components/Navigationbar.vue'
import axios from 'axios'

export default {
    components: {
        navbar,
    },
    data() {
        return {
            users: [],
            errors: [],
            baseUrl: "http://127.0.0.1:8000/api",
            deleteduser: {},
            headers: {
                Authorization : `Bearer ${localStorage.getItem("token")}`,
                Accept: "application/json"
            }
        }
    },
    async mounted() {

        try {
            const response = await axios.get(this.baseUrl + '/getUserPhoneTown', {headers: this.headers});
            this.users = response.data.requestdata;
        } catch (error) {
            this.errors.push(error);
        }
    },
    methods: {
        async deleteuser(userid) {
            console.log(userid);
            try {
                const response = await axios.delete(this.baseUrl + '/deleteUser?id=' + userid, {headers: this.headers});
                // console.log(response.data);
            } catch (error) {
                this.errors.push(error);
                // console.log("The error is: " + this.errors[this.errors.length]);
            }

            window.location.reload();
        }
    }
}
</script>

<style scoped>
.table-position {
    margin-top: 37px;
    margin-bottom: 40px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: start;
    padding-left: 2%;
    padding-right: 2%;
}

.table-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: start;
    border: 3px solid rgb(66, 66, 66);
    border-radius: 25px;
    width: 100%;
    overflow: hidden;
}

.table-title {
    background-color: rgb(182, 182, 182);
    width: 100%;
    display: flex;
    justify-content: center;
    text-align: center;
}

.table-header {
    display: flex;
    flex-direction: row;
    align-items: end;
    width: 100%;
    border-bottom: 3px solid rgb(66, 66, 66);
    border-top: 3px solid rgb(66, 66, 66);
}

.table-body {
    display: flex;
    flex-direction: row;
    border-bottom: 2px solid black;
    width: 100%;
    height: fit-content;
    transition: background-color 0.2s ease-in-out
}

.table-body:hover,
.table-body:focus {
    background-color: rgb(159, 159, 159);
}

.header-cell {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgb(112, 112, 112);

}

.header-cell:hover,
.header-cell:focus {
    background-color: rgb(169, 213, 240);
}

.body-cell:hover,
.body-cell:focus {
    background-color: rgb(169, 213, 240);
}

.cell {
    min-width: 70px;
    height: auto;
    word-wrap: break-word;
    padding: 6px;
    transition: background-color 0.3s ease-in-out;
}

.username-column {
    width: 25%;
    border-right: 2px solid black;
}

.email-column {
    width: 43%;
    border-right: 2px solid black;
}

.phonenumber-column {
    width: 10%;
    border-right: 2px solid black;
}

.town-column {
    width: 10%;
    border-right: 2px solid black;
}

.actions-column {
    width: 12%
}

.action-record {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
}

.table-button {
    padding: 4px;
    height: 35px;
    width: 65px;
    margin-top: 3px;
    margin-bottom: 3px;
    font-size: 95%;
    border: 3px solid rgb(97, 97, 97);
    border-radius: 14px;
    background-color: rgb(176, 176, 176);
    transition: background-color 0.7s, box-shadow 0.7s ease-in-out;
    box-shadow: 1.8px 2.5px 3.4px 0.5px rgba(0, 0, 0, 0.6);
    cursor: pointer
}

.update-button:hover {
    color: white;
    background-color: rgb(86, 125, 205);
    box-shadow: 3.8px 2.5px 8.4px 0.5px rgba(86, 125, 205, 0.8)
}

.delete-button:hover {
    color: white;
    background-color: rgb(239, 63, 63);
    box-shadow: 3.8px 2.5px 8.4px 0.5px rgba(239, 63, 63, 0.8)
}
</style>