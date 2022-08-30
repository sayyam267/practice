<!-- testing computed vs methods -->
<template>
    <div>
        {{name}}
        <input type="text" v-model="item" placeholder="enter item">
        <div>{{reverse}}</div>
        <div v-if="typing">Typing</div>
        <!-- <div>Random Number from method{{getRandom()}}</div>
        <div>Random Number from method{{getRandom()}}</div>
        <div>Random Number from method{{getRandom()}}</div>
        <div>Random no form computed property{{getRandom1}}</div>
        <div>Random no form computed property{{getRandom1}}</div>
        <div>Random no form computed property{{getRandom1}}</div> -->
        
        <input type="text" v-model="stName" placeholder="enter Student Name">
        <input type="text" v-model="stClass" placeholder="enter class">
        <button @click="addStudent">Add Student</button>

        
        <div> <input type="text" v-model="Gb" placeholder="enter Student Name"> <br/> ->  : {{mb}}Mb</div>


        <!-- slot used in student component  -->

        <div>
            <Students msg="Students" :student="students"><span slot="title">Table</span> <h2 slot="subtitle">ABC SCHOOL Students Records</h2></Students>
        </div>
        
        </div>
</template>

<script>
import Students from '../components/Students.vue';

    export default {
        name:'TestProperties',
        components:{
    Students,
},
       
        data(){
            return{
                name:'test',
                 item:'hello',
                 typing:false,
                 stName:'',
                 stClass:'',
                 students:[{studentName:'sayyam',class:'12'}],
                 Gb:null,
                 mb:null,
            }
        },

        methods:{
            getRandom: function(){
                return Math.random();
            },

            addStudent: function(){
                this.students.push({studentName:this.stName,class:this.stClass});
                this.stName='';
                this.stClass='';
            }
        },

        computed:{
            getRandom1: function(){
                
                return Math.random();
            },
            reverse: function(){
                return this.item.split('').reverse().join('');
            }
            
        },

        watch:{
            $route(){
                this.$route.name
                console.log("heee");
                setTimeout(() => {
                    this.typing = false;
                }, 2000);
            },

            Gb(){
                this.mb= this.Gb * 1024;
            }
        }
    }
</script>

<style scoped>
    
</style>