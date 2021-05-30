<template>
    <header> 
        <h1 align="center">{{title}}</h1>
        <div id="nav">
            <router-link to="/">Список</router-link> |
            <router-link to="/about">Статистика</router-link>
        </div>
    </header>
</template>

<script>
import Button from './Button'
import request from 'request-promise';

export default {
    name: 'Header',
    props: {
        title: {
            type: String,
            default: 'Hello world',
        },
    },
    components: {
        Button
    },  
    data() {
        return {
            url: process.env.VUE_APP_API_URL,
        }
    },
    computed: {
        homePage() {
            return ['/', '/update-bypass'].includes(this.$route.path);
        }
    },
    methods: {
        async Logout() {
            console.log(localStorage.getItem('token'), this.headers)
            if (localStorage.getItem('token')) {
                await request.get(`${this.url}/logout`, { 
                    headers: {
                        Authorization: localStorage.getItem('token'),
                    } 
                });
                localStorage.removeItem('token');
            }
            this.$router.push({ name: 'Login' });
        }
    }
}
</script>

<style scoped>
    header {
        flex-direction: column;
        justify-content: center;
        display: flex;
        align-items: center;
        margin-bottom: 20px;
    }
</style>