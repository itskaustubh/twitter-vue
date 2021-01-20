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
            <form class = "user-profile__create_tweet" @submit.prevent="createTweet">
              <label for="newTweet"><strong>New Tweet</strong> 
                <div id='char-count' :class="{ '--exceeded' : charCount > 180 }" v-if="charCount > 0"> ({{charCount}}/180)</div>
              </label>
              <textarea style="resize:none" id="newTweet" rows="4" v-model="newTweetContent" />

              <div class="user-profile__create-tweet-type"> 
                <label for='tweetType'><strong>Type: </strong> </label>
                <select id="tweetType" style="margin-top : 15px" v-model="newTweetType"> 
                  <option v-for="option in tweetType" :key='option.value' :value="option.value">
                    {{option.name }}  
                  </option>
                </select>
              </div>
              <button id = 'tweet-button' v-if="newTweetType == 'instant' && charCount <= 180">Tweet</button>
            </form> 
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
      },
      tweetType: [
        {value : 'instant', name: 'Instant Tweet'},
        {value : 'draft', name : 'Draft'},
      ],
      newTweetContent : '',
      newTweetType : 'instant',
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
    charCount(){
      return this.newTweetContent.length
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
    },
    createTweet(){
      if (this.newTweetContent && this.newTweetType != 'draft'){
        this.user.tweets.unshift({
          id: this.user.tweets.length + 1,
          text: this.newTweetContent
        });
        this.newTweetContent = ''
        console.log(this.user.tweets)
      }
    }
  },
  mounted(){
    this.followers = 42;
  }
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

      .user-profile__create_tweet{
        padding-top: 15px;
        display: flex;
        flex-direction: column;

          #tweet-button {
          margin-top: 20px;
          width: 100px;
          padding: 5px 0 5px 0;
          

          background: #3498db;
          background-image: -webkit-linear-gradient(top, #3498db, #2980b9);
          background-image: -moz-linear-gradient(top, #3498db, #2980b9);
          background-image: -ms-linear-gradient(top, #3498db, #2980b9);
          background-image: -o-linear-gradient(top, #3498db, #2980b9);
          background-image: linear-gradient(to bottom, #3498db, #2980b9);
          -webkit-border-radius: 28;
          -moz-border-radius: 28;
          border-radius: 28px;
          font-family: Arial;
          color: #ffffff;
          font-size: 15px;
          text-decoration: none;

          &:hover {
            background: #3cb0fd;
            background-image: -webkit-linear-gradient(top, #3cb0fd, #3498db);
            background-image: -moz-linear-gradient(top, #3cb0fd, #3498db);
            background-image: -ms-linear-gradient(top, #3cb0fd, #3498db);
            background-image: -o-linear-gradient(top, #3cb0fd, #3498db);
            background-image: linear-gradient(to bottom, #3cb0fd, #3498db);
            text-decoration: none;
          }
        }

        .--exceeded{
          color: red;
          }
      }
  }
}


h1{
    margin: 0;
}
</style>
