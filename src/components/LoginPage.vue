<template>
    <img src="../assets/logo.png" id="logo">
    <h1>Login</h1>
    <div id="login">
        <input type="text" v-model="email" placeholder="Enter Email" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button @click="login">Login</button>
        <p>
            <router-link to="/sign-up">Sign Up</router-link>
        </p>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'LoginPage',
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        async login() {
            let result = await axios.get(`YOUR LOCALHOST ADDRESS/users?email=${this.email}&password=${this.password}`)
            if (result.status == 200 && result.data.length > 0) {
                localStorage.setItem("user-info",JSON.stringify(result.data[0]))
                this.$router.push({ name: 'HomePage' })
            }
            console.log(result)
        }
    }
}
</script>
