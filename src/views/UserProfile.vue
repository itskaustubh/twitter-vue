<template>
  <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">
                @{{ username }}
                <div class = "user-profile__verified" v-if="user.isVerified">
                    <img src='../assets/verified.svg' alt = 'Verified' height="20" width="20">
                </div>
            </h1>
            <div class="user-profile_follower-count">
                <strong>Followers: </strong> {{followers}}
            </div>
           <CreateTweetPanel @tweetText='createTweet'/>
        </div>  
        <TweetItem 
        v-for="tweet in user.tweets" 
        :key="tweet.id" 
        :username="user.username" 
        :tweet='tweet'
        @favourite='toggleFavourite'
        />
  </div>
</template>


<script>
import TweetItem from '../components/TweetItem';
import CreateTweetPanel from '../components/CreateTweetPanel'
import { useRoute} from 'vue-router';
import {ref,computed,watch, onMounted} from 'vue';
import {users} from '../assets/users.js'

export default {
  name: 'UserProfile',
  components: { TweetItem,CreateTweetPanel},

  setup(){

    const route = useRoute();
    const username = computed(() => route.params.username);

    const followers = ref(0);
    console.log(users)
    const user = ref(users[username.value] || users['kaustubh'])

      const fullName = computed(() => `${user.value.firstName} ${user.value.lastName}`);

      watch(function (newCount,oldCount){
      if (oldCount < newCount){
        console.log(`You now have ${followers.value} followers`)
      }
    });

    function followUser() {
      followers.value++;
    }

    function toggleFavourite(id){
      console.log(`Tweet #${id} favourited`);
    }
    function createTweet(newTweetContent){
      user.value.tweets.unshift({
      id: user.value.tweets.length + 1,
      text: newTweetContent
      });
      console.log(user.value.tweets)
    }

    onMounted(() => followers.value = 42);


      return {
        followers,
        user,
        fullName,
        followUser,
        toggleFavourite,
        createTweet,
        username
      }

  },
  
  // data() {
  //   return {
  //     followers: 0,
  //     user: {
  //       id: 1,
  //       username: 'kaustubh',
  //       firstName: 'Kaustubh',
  //       lastName: 'Bhagwat',
  //       email: 'hello@kaustubh.app',
  //       isVerified: true,
  //       tweets: [
  //         { id:1, text: "Man.. Ninjas are cool. I just don't know any personally" },
  //         { id:2, text: "Sometimes I get emotional over fonts"},
  //                   { id:3, text: "Man.. Ninjas are cool. I just don't know any personally" },
  //         { id:4, text: "Sometimes I get emotional over fonts"}
  //       ]
  //     },
  //   }
  // },
  // computed: {
  //   fullName() {
  //     return `${this.user.firstName} ${this.user.lastName}`;
  //   },
  // },
  // watch: {
  //   followers(newCount,oldCount){
  //     if (oldCount < newCount){
  //       console.log(`You now have ${this.followers} followers`)
  //     }
  //   }
  // },
//   methods: {
//     followUser() {
//       this.followers++;
//     },
//     toggleFavourite(id){
//       console.log(`Tweet #${id} favourited`);
//     },
//     createTweet(newTweetContent){
//       this.user.tweets.unshift({
//       id: this.user.tweets.length + 1,
//       text: newTweetContent
//       });
//       console.log(this.user.tweets)
// }
//   },
  // mounted(){
  //   this.followers = 42;
  // }
}
</script> 

<style lang='scss' scoped>

.user-profile{
    /* display: grid;
    grid-template-columns: 1fr 3fr; */
    width: 100%;
    padding: 50px 5%;

  .user-profile__user-panel{
      display: flex;
      flex-direction: column;
      margin-right: 50px;
      padding: 20px;
      background-color: white;  
      border-radius: 5px;
      border: 1px solid #DFE3E8;

      .user-profile__username{
        display: flex;
        flex-direction: row;
      }
  }
}
</style>
