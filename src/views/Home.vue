<template>
  <div class="container">
    <list :superheroList="finalList" />
    <Panel />
  </div>
</template>

<script>
import axios from 'axios'

import List from '@/components/List.vue'
import Panel from '@/components/Panel.vue'

export default {
  name: 'Home',
  components: {
    List,
    Panel
  },

  data() {
    return {
      baseURL: 'http://157.245.138.232:9091/api/v1/test/superheroes',
      superheroList: []
    }
  },

  computed: {
    finalList() {
      return this.superheroList
    }
  },
  methods: {
    async getSuperheroList() {
      const res = await axios.get(this.baseURL)
      console.log('response ALL', res)
      this.superheroList = res.data.data
    },

    async getSuperheroById(id) {
      const res = await axios.get(`${this.baseURL}/${id}`)
      console.log('response by ID', res)
    },

    async getSuperheroByAbilities(flying) {
      const res = await axios.get(`${this.baseURL}?puedeVolar=${flying}`)
      console.log('response by Abilities', res)
    }
  },

  mounted() {
    this.getSuperheroList()

    this.getSuperheroById(1)

    this.getSuperheroByAbilities(true)
  }
}
</script>

<style lang="scss">
.container {
  height: 100vh;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
</style>
