<template>
  <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">
                @{{ user.username }}
                <div class = "user-profile__verified" v-if="user.isVerified">
                    <img src='../assets/verified.svg' alt = 'Verified' height="20" width="20">
                </div>
                </h1>

            <div class="user-profile_follower-count">
                <strong>Followers: </strong> {{followers}}
            </div>
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
import TweetItem from './TweetItem';

export default {
  name: 'UserProfile',
  components: { TweetItem},
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: 'kaustubh',
        firstName: 'Kaustubh',
        lastName: 'Bhagwat',
        email: 'hello@kaustubh.app',
        isVerified: true,
        tweets: [
          { id:1, text: "Man.. Ninjas are cool. I just don't know any personally" },
          { id:2, text: "Sometimes I get emotional over fonts"},
                    { id:3, text: "Man.. Ninjas are cool. I just don't know any personally" },
          { id:4, text: "Sometimes I get emotional over fonts"}
        ]
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  watch: {
    followers(newCount,oldCount){
      if (oldCount < newCount){
        console.log(`You now have ${this.followers} followers`)
      }
    }
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id){
      console.log(`Tweet #${id} favourited`);
    }
  },
  mounted(){
    this.followers = 42;
  }
}
</script> 

<style>

.user-profile{
    /* display: grid;
    grid-template-columns: 1fr 3fr; */
    width: 100%;
    padding: 50px 5%;
}

.user-profile__user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile__username{
    display: flex;
    flex-direction: row;
}

h1{
    margin: 0;
}


</style>
