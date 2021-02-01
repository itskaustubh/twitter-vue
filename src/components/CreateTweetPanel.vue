<template>
     <form class = "user-profile__create_tweet" @submit.prevent="returnTweetText">
              <label for="newTweet"><strong>New Tweet</strong> 
                <div id='char-count' :class="{ '--exceeded' : charCount > 180 }" v-if="charCount > 0"> ({{charCount}}/180)</div>
              </label>
              <textarea id="newTweet" rows="4" v-model="newTweetContent" />

              <div class="user-profile__create-tweet-type"> 
                <label for='tweetType'><strong>Type: </strong> </label>
                <select id="tweetType" v-model="newTweetType"> 
                  <option v-for="option in tweetType" :key='option.value' :value="option.value">
                    {{option.name }}  
                  </option>
                </select>
              </div>
              <button id = 'tweet-button' v-if="newTweetType == 'instant' && charCount <= 180">Post</button>
            </form> 
</template>

<script>
import {ref,computed} from 'vue';

export default {
    name: 'CreateTweetPanel',
    setup(_,context) {  

        const tweetType = ref([
                {value : 'instant', name: 'Instant Tweet'},
                {value : 'draft', name : 'Draft'},
            ]);
        const newTweetContent = ref('');
        const newTweetType = ref('instant');


        const charCount = computed(() => newTweetContent.value.length);

        function returnTweetText() {
            if (newTweetContent.value && newTweetType.value != 'draft'){
                context.emit('tweetText',newTweetContent.value);
            }
            newTweetContent.value = ''
            console.log('Tweet returned')
        }

        return{
            tweetType,
            newTweetContent,
            newTweetType,
            charCount,
            returnTweetText,
        }
    }
}
</script>

<style lang='scss' scoped>
    .user-profile__create_tweet{
    padding-top: 15px;
    display: flex;
    flex-direction: column;

        #tweet-button {
        margin-top: 20px;
        width: 100px;
        padding: 5px 0 5px 0;
        background: deeppink;
        -webkit-border-radius: 28;
        -moz-border-radius: 28;
        border-radius: 28px;
        font-family: Arial;
        color: #ffffff;
        font-size: 15px;
        font-weight: bold;

        &:hover {
        background: rgb(255, 68, 168);
        text-decoration: none;
        }
    }

    #tweetType{
        margin-top: 15px;
    }

    .--exceeded{
        color: red;
        }
    }

    textarea{
        resize: none;
    }
</style>