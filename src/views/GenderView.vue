
<template>
    <div id="Gender">
        <div>
      <h1 >Gender Predictor </h1>
      <h4>Predict gender by name</h4>
    </div>
        <img src="../assets/gender.png" alt="">
        <div>
            <input
                :style="{ marginTop: '10px', border: '2px solid #42b983', minWidth: '20%', padding: '10px'}"
                type="text" v-model="name" placeholder="enter name">
        </div>
        <div :style="{margin:'auto',width:'21.6%',textAlign: 'left',marginTop:'1px'}"><h4 v-if="error" :style="{color:'red',fontSize:'10px',marginTop:'2px'}">Please enter name</h4></div>

        <button v-if="!loading" class="btn" @click="CheckGender">
            Check Gender
        </button>
        <button v-else class="btn">
            Loading
        </button>

        <div :style="{border:'1px solid #42b983',padding:'20px',margin:'auto', marginTop: '10px', maxWidth:'30%'}"
            v-if="isShow">
            <h3 v-if="gender === 'male'">{{myName}} your gender is <span :style="{ color: '#2ee88e' }">Male</span></h3>
            <h3 v-else-if="gender === 'female'" >{{myName}} your gender is <span :style="{ color: '#2ee88e' }">Female</span></h3>
        </div>


    </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import axios from 'axios';

export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Gender",
    data: () => {
        return {
            name: "",
            gender: "",
            isShow: false,
            check: false,
            loading:false,
            error:false,
            myName:'',
            style: {
                backgroundColor: '#42b983'
            }
        }
    },
    methods: {
        CheckGender() {
            if(this.name === ''){
                this.error = true;
                this.isShow = false;
            }
            else{
                console.log("CheckGender call", this.name);
                this.myName=this.name;
                this.error=false;
                this.loading =true;
                this.isShow = false;
            axios
                .get(`https://api.genderize.io?name=${this.name}`)
                .then(response => {console.log(response?.data.gender);this.gender=response.data.gender; this.isShow = true;this.loading = false;})
            }
            
        }
    }
};
</script>


<style>
#Gender {
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
    min-width: 21.5%;
    margin-top: 10px;
    padding: 10px;
    border: 2px solid #42b983;
    font-size: 16px;
}

.btn:hover {
    background-color: #fff;
    color: #2c3e50
}
img{
    height:13%;
    width:13%;
}
</style>
