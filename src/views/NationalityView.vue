<template>
  <div id="Nationality">
    <div>
      <h1>Nationality Predictor</h1>
      <h4>Predict Nationality by name</h4>
    </div>
    <img src="../assets/nationality.jpg" alt="" />
    <div>
      <input
        :style="{
          marginTop: '10px',
          border: '2px solid #42b983',
          minWidth: '20%',
          padding: '10px',
        }"
        type="text"
        v-model="name"
        placeholder="enter name"
      />
    </div>
    <div
      :style="{
        margin: 'auto',
        width: '21.6%',
        textAlign: 'left',
        marginTop: '1px',
      }"
    >
      <h4
        v-if="error"
        :style="{ color: 'red', fontSize: '10px', marginTop: '2px' }"
      >
        Please enter name
      </h4>
    </div>

    <button v-if="!loading" class="btn" @click="CheckNationality">
      Check Nationality
    </button>
    <button v-else class="btn">Loading</button>
<h3 :style="{fontSize:'20px'}" v-if="isShow"> Nationality of {{myName}} is given below</h3>
    <table  v-if="isShow" :style="{marginTop:'5px'}">
        <thead >
          <tr>
            <th>#</th>
            <th>Country Code</th>
            <th>Country Flag</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(entry, i) in country" :key="i">
            <td >{{ ++i }}</td>
            <td>{{ entry?.country_id }}</td>
            <td> <img :src="'https://countryflagsapi.com/png/'+entry.country_id" alt="img" /></td>
          </tr>
        </tbody>
      </table>
  
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import axios from "axios";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Nationality",
  data: () => {
    return {
      name: "",
      country: [],
      isShow: false,
      check: false,
      loading: false,
      error: false,
      myName: "",
      style: {
        backgroundColor: "#42b983",
      },
    };
  },
  methods: {
    CheckNationality() {
      if (this.name === "") {
        this.error = true;
        this.isShow = false;
      } else {
        console.log("CheckGender call", this.name);
        this.myName = this.name;
        this.error = false;
        this.loading = true;
        this.isShow = false;
        axios
          .get(`https://api.nationalize.io?name=${this.name}`)
          .then((response) => {
            console.log(response?.data?.country);
            this.country = response?.data?.country;
            console.log(this.country);
            this.isShow = true;
            this.loading = false;
          });
      }
    },
  },
};
</script>

<style>
#Nationality {
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
  background-color: #42b983;
  color: #2c3e50;
}
img {
  height: 15%;
  width: 15%;
}
td{
    border: 1px solid #ddd;
    padding: 8px;
}
th{

  padding-top: 12px;
  padding-bottom: 12px;
  /* text-align: left; */
  background-color: #04AA6D;
  color: white;
}

table{
  border-collapse: collapse;
  width: 50%;
  margin: auto;
  margin-top: 10px;
}
</style>
