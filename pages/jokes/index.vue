<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>
import Joke from '../../components/joke'
import SearchJokes from '../../components/SearchJokes'
export default {
  components: {
    Joke,
    SearchJokes
  },
  data() {
    return {
      jokes: []
    }
  },
  async created() {
    const config = {
      headers: {
        Accept: 'application/json'
      }
    }
    try {
      const res = await this.$axios.get(
        'https://icanhazdadjoke.com/search',
        config
      )
      this.jokes = res.data.results
    } catch (err) {
      console.log(err)
    }
  },
  methods: {
    async searchText(Text) {
      const config = {
        hedaers: {
          Accept: 'application/json'
        }
      }
      try {
        const res = await this.$axios.get(
          'https://icanhazdadjoke.com/search?term=${text}',
          config
        )
        this.jokes = res.data.results
      } catch (err) {
        console.log(err)
      }
    }
  },
  head() {
    return {
      title: 'Dad Jokes',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Best Place for corny dad jokes'
        }
      ]
    }
  }
}
</script>

<style></style>
