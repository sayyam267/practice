
<template>
    <div id="Login">
        <img src="../assets/logo.png" alt="">
        <div>
            <AboutUs msg="Login Form" />
        </div>
        <div v-if="isShow">
            <h3 v-if="check" :style="{ color: '#2ee88e' }">Login Success</h3>
            <h3 v-else :style="{ color: '#ed3734' }">Invalid Details</h3>
        </div>

        <!-- <input :value="text" @input="event => text = event.target.value"> -->
        <div>
            <input
                :style="{ marginTop: '10px', border: '2px solid #42b983', minWidth: '20%', padding: '10px', }"
                type="text" v-model="email" placeholder="enter email">
        </div>
        <div>
            <input
                :style="{ border: '2px solid #42b983', minWidth: '20%', marginTop: '10px', padding: '10px', }"
                type="password" v-model="pass" placeholder="enter Password">

        </div>


        <button class="btn" @click="Login">
            <Icon icon="ant-design:login-outlined" /> Login
        </button>

        <!-- <Icon icon="mdi-light:home" /> -->


    </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import AboutUs from "./AboutUs.vue";
import { Icon } from '@iconify/vue2';

export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Login",
    components: {
        Icon,
        AboutUs,
    },
    data: () => {
        return {
            name: "",
            email: "",
            pass: "",
            isShow: false,
            check: false,
            style: {
                backgroundColor: '#42b983'
            }
        }
    },
    methods: {
        Login() {
            console.log("Login call", this.email, this.pass);
            this.isShow = true;
            if (this.email === "sayyam" && this.pass === "1234") {
                this.$router.push('gender-check')
                this.check = true;
            }
        }
    }
};
</script>


<style>
#Login {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 50px;
}

.btn {
    background-color: #42b983;
    color: white;
    min-width: 20%;
    margin-top: 10px;
    padding: 10px;
    border: 2px solid #42b983;
    font-size: 16px;
}

.btn:hover {
    background-color: #fff;
    color: #2c3e50;
}
</style>
