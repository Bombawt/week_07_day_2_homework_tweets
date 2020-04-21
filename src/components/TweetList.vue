<template lang="html">

  <div id="app">

  <h2>{{ tweet.name }}</h2>
  <h3>{{ tweet.handle }}</h3>
  <img :src="tweet.img" width="100" height="100">
  <p>{{ tweet.tweet }}</p>
  <p>{{ tweet.likes }} likes</p>
</div>
</template>

<script>
export default {
  name: 'tweet-list',
  props: ['tweet']
}
</script>

<style lang="css" scoped>
</style>
