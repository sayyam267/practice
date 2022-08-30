<template>
    <div class="Students">
        <h1>{{  msg  }} <slot name="title" ></slot></h1>
        <slot name="subtitle"></slot>
        
        <table  :style="{marginTop:'5px'}">
        <thead >
          <tr>
            <th>#</th>
            <th>Student Name</th>
            <th>Class</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(entry, i) in student" :key="i">
            <td >{{ ++i }}</td>
            <td>{{ entry?.studentName }}</td>
            <td>{{entry?.class}}</td>
          </tr>
        </tbody>
      </table>
    </div>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Students',
    props: {
        msg: String,
        student:Array
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
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
