<template>
    <div>
        <div v-if="loading">
            <span>loading...</span>
        </div>
        <div v-else>
        <nuxt-link to="/jokes">
        Back to Jokes
        </nuxt-link>
        <h2 v-if="joke">{{ joke }}</h2>
        <hr>
        <small>Joke ID: {{ $route.params.id }}</small>
        </div>
    </div>
</template>

<script>
// import axios from 'axios';

export default {
    data() {
        return {
            joke: '',
            loading: false
        }
    },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
        this.loading = true;
      const res = await this.$axios.get(
        `https://icanhazdadjoke.com/j/${this.$route.params.id}`,
        config
      );
      this.joke = res.data.joke;
      this.loading = false;
    } catch (err) {
      console.log(err);
    }
  },     
    head() {
        return {
            title: this.joke,
            meta: [
                {
                    hid: "description",
                    name: "description",
                    content: "Best Place for corny dad jokes"
                    }
                    ]
                    };
                    }
    
};
</script> 


<style>

</style>