<template>
  <div>
    <button @click="getStudents">获取信息</button>
    <button @click="getCars">获取信息</button>
  </div>
</template>

<script>
  import axios from "axios"
  export default {
      name: 'App',
      methods: {
        getStudents(){
          axios.get('http://localhost:8080/control/students').then(
            response => {
              console.log("yes",response.data)
            },
            error => {
              console.log("no",error.message)
            }
          )
        },
        getCars(){
          axios.get('http://localhost:8080/con/cars').then(
            response => {
              console.log("yes",response.data)
            },
            error => {
              console.log("no",error.message)
            }
          )
        }
      },
  }
</script>

<style>
   
</style>