<template>
  <div class="home">
    Home 
      <div class= 'usernames'>
    <router-link v-for="user in users" :key="user" :to="{name: 'UserProfile', params: {username: user['username']}}">
      {{user['username']}}
    </router-link> 
  </div>
  </div>

</template>

<script>
// import { useRoute} from 'vue-router';
// import {ref,computed,watch, onMounted} from 'vue';
import {users} from '../assets/users.js'

export default {
  name: 'Home',
  setup(){
    console.log(users)
    for(var user in users){
      console.log(user)
    }
    return {
      users
    }
  }
}


</script>

<style lang="scss" scoped>
  .home{
    padding: 50px 5%;
    font-size: 24px;
    background: white;
  }

  .usernames{
    padding-top: 50px;
    display: flex;
    flex-direction: column;
  }
</style>