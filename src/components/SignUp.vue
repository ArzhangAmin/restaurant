<template>
    <img src="../assets/logo.png" id="logo">
    <h1>Sign Up</h1>
    <div id="register">
        <input type="text" v-model="name" placeholder="Enter Name" />
        <input type="text" v-model="email" placeholder="Enter Email" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button @click="SignUp">Sign Up</button>
        <p>
            <router-link to="/login">Login</router-link>
        </p>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'SignUp',
    data() {
        return {
            name: '',
            email: '',
            password: ''
        }
    },
    methods: {
        async SignUp() {
            let result = await axios.post("YOUR LOCALHOST ADDRESS/users",{
                name: this.name,
                email: this.email,
                password: this.password
            });

            if (result.status == 201) {
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({ name: 'HomePage' })
            }
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (user) {
            this.$router.push({ name: 'HomePage' })
        }
    }
}
</script>

