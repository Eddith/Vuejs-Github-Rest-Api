<template>
  <div class="container">
    <h1 class="text-center">Github Rest Api</h1>
    <input style="margin: 20px auto; display: block;" placeholder="User Name Giriniz..." type="text" v-model="users">
    <button 
      style="margin: 1px auto; display: block;" 
      type="button" 
      class="btn btn-xs bt-primary" 
      @click="searchName">Getir</button>
    <div class="card" :style="this.display" style="width: 18rem; margin: 20px auto; display: block;">
      <div class="card-body"> 
        <h5 class="card-title text-center">{{ this.name }}</h5>
        <p class="card-text">Fallowers : {{ this.fallowers }}</p>
        <p class="card-text">Fallowing : {{ this.fallowing }}</p>
        <p class="card-text">Location : {{ this.location }}</p>
        <p class="card-text">Repos : {{ this.repos }}</p>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data() {
      return {
        users: '',
        name: '',
        fallowers: null,
        fallowing: null,
        location: null,
        repos: null,
        display: 'display: none;'
      }
    },
    methods : {
      searchName(){
        if(this.users === null){
          this.display = 'display: none;'
          alert("Lütfen kullanıcı adı giriniz!!!")
        } else {
          let userName = this.users
          axios.get(`https://api.github.com/users/${userName}`)
            .then(response => {
              console.log(response.data)
              this.display = 'display: block;'
              this.name = response.data.name
              this.fallowers = response.data.followers
              this.fallowing = response.data.following
              this.location = response.data.location
              this.repos = response.data.public_repos
            })
        }
      }
    },
    created(){
      axios.get("https://api.github.com/users")
        .then(response => {
          console.log(response.data)
        })
    }
  }
</script>

<style scoped>

</style>