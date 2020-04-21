<template lang="html">
  <div id="app">
  <h1>Tweet List</h1>

  <h2>Total Likes: {{ totalLikes }}</h2>

  <form v-on:submit.prevent="saveTweet">
      <h3>Add a new Tweet</h3>
      <input placeholder="Name" type="text" v-model="newTweet.name"/>
      <input placeholder="Handle" type="text" v-model="newTweet.handle"/>
      <input placeholder="Avatar URL" type="text" v-model="newTweet.img"/>
      <input placeholder="Tweet Text" type="text" v-model="newTweet.tweet"/>
      <input placeholder="Number of Likes" type="number" v-model.number="newTweet.likes"/>
      <input type="submit" value="Add Tweet"/>
    </form>


  <div id="filterTweets">
  <h3>Filter Tweets by number of likes</h3>
  <input type="number" v-model.number="filterAmount">
  </div>
      <div class="tweet" v-for="tweet in filteredTweets">
        <h2>{{ tweet.name }}</h2>
        <h3>{{ tweet.handle }}</h3>
        <img :src="tweet.img" width="100" height="100">
        <p>{{ tweet.tweet }}</p>
        <p>{{ tweet.likes }} likes</p>
      </div>
      <tweet-list v-for="(tweet, index) in tweets" :key="index" :tweet="tweet"></tweet-list>
</div>


</template>

<script>

import TweetList from './components/TweetList.vue';

export default {
  data() {
    return {
      tweets:[
        {
          id: 1,
          name: 'James',
          handle: '@jokerjames',
          img: 'https://semantic-ui.com/images/avatar2/large/matthew.png',
          tweet: "If you don't succeed, dust yourself off and try again.",
          likes: 10,
        },
        {
          id: 2,
          name: 'Fatima',
          handle: '@fantasticfatima',
          img: 'https://semantic-ui.com/images/avatar2/large/molly.png',
          tweet: 'Better late than never but never late is better.',
          likes: 12,
        },
        {
          id: 3,
          name: 'Xin',
          handle: '@xeroxin',
          img: 'https://semantic-ui.com/images/avatar2/large/elyse.png',
          tweet: 'Beauty in the struggle, ugliness in the success.',
          likes: 18,
        }
      ],
      newTweet: {
        name: "",
        handle: "",
        img: "",
        tweet: "",
        likes: 0
      },
      filterAmount: 0
    }
  },
  components: {
    'tweet-list': TweetList
  },
  computed: {
    totalLikes: function(){
      return this.tweets.reduce((total, tweet) => total + tweet.likes, 0 );
    },
    filteredTweets: function(){
      return this.tweets.filter((tweet) => {
        return tweet.likes >= this.filterAmount
      })
    },
  },
methods: {
      saveTweet: function(){
        this.tweets.unshift(this.newTweet);

        this.newTweet = {
          name: "",
          handle: "",
          img: "",
          tweet: "",
          likes: 0
        };
      }
    }
}
</script>

<style lang="css" scoped>
</style>
