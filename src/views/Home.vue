<template>
  <div class="container">Hello W!</div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Home',
  components: {},

  data() {
    return {
      baseURL: 'http://157.245.138.232:9091/api/v1/test/superheroes',
      list: []
    }
  },

  computed: {},
  methods: {
    async getSuperheroList() {
      const res = await axios.get(this.baseURL)
      console.log('response', res)
    }
  },

  mounted() {
    this.getSuperheroList()
  }
}
</script>

<style lang="scss">
.container {
  background-color: gray;
  height: 100vh;
}
</style>
