<template>
    <HeaderElement />
    <h1>Hello User, Welcome on Add Restaurant Page</h1>
    <form id="add">
        <input type="text" name="name" placeholder="Enter Name" v-model="restaurant.name" />
        <input type="text" name="address" placeholder="Enter Address" v-model="restaurant.address" />
        <input type="text" name="contact" placeholder="Enter Contact" v-model="restaurant.contact" />
        <button @click="addRestaurant" type="button">Add new Restaurant</button>
    </form>
</template>

<script>
import HeaderElement from './HeaderElement.vue';
import axios from 'axios';
export default {
    name: 'AddRestaurant.vue',
    components: { HeaderElement },
    data() {
        return {
            restaurant: {
                name: '',
                address: '',
                contact: ''
            }
        }
    },
    methods: {
        async addRestaurant() {
            const result = await axios.post("YOUR LOCALHOST ADDRESS/restaurants",{
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact,
            });
            if (result.status == 201) {
                this.$router.push({ name: 'HomePage' })
            }
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: 'SignUp' })
        }
    }
}
</script>

