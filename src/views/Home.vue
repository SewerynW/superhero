<template>
  <div class="container">
    <div v-if="showErrorInfo" class="errorInfo">
      <p>
        Something went wrong with fetching pictures.<br />
        We change picture for default picture.
      </p>
      <button @click="showErrorInfo = false">close</button>
    </div>

    <list @showBox="showError" :superhero-list="filteredList" />
    <Panel
      @enteredId="updateId"
      @pickedAbility="updateAbility"
      @entereNickname="updateNickname"
    />
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
      heroList: [],
      heroListById: [],
      heroListByAblitiy: [],
      selectedId: null,
      selectedAbility: '',
      selectedNickname: '',
      showErrorInfo: false
    }
  },

  computed: {
    mergedList() {
      const list = [].concat(
        this.heroList,
        this.heroListById,
        this.heroListByAblitiy
      )

      return list.reduce((acc, hero) => {
        if (acc.some((checkedHero) => checkedHero.id === hero.id)) {
          return acc
        } else {
          acc.push(hero)
          return acc
        }
      }, [])
    },

    filteredList() {
      return this.mergedList.filter((hero) => {
        return hero.nombre
          .toLowerCase()
          .includes(this.selectedNickname.toLowerCase())
      })
    }
  },

  watch: {
    selectedId(value) {
      this.getSuperheroById(value)
    },

    selectedAbility(value) {
      switch (value) {
        case 'canFly':
          this.heroList = []
          this.getSuperheroByAbilities(true)
          break
        case 'canNotFly':
          this.heroList = []
          this.getSuperheroByAbilities(false)
          break
        case 'all':
          this.getSuperheroList()
          break
        default:
          break
      }
    }
  },
  methods: {
    showError() {
      this.showErrorInfo = true
    },

    updateId(value) {
      this.selectedId = value
    },

    updateAbility(value) {
      this.selectedAbility = value
    },

    updateNickname(value) {
      this.selectedNickname = value
    },

    async getSuperheroList() {
      try {
        const response = await axios.get(this.baseURL)
        this.heroList = response.data.data
      } catch (er) {
        console.error(er)
        return
      }
    },

    async getSuperheroById(id) {
      try {
        const response = await axios.get(`${this.baseURL}/${id}`)
        this.heroListById = response.data.data
      } catch (er) {
        this.heroListById = []
        console.error(er)
        return
      }
    },

    async getSuperheroByAbilities(flying) {
      try {
        const response = await axios.get(`${this.baseURL}?puedeVolar=${flying}`)
        this.heroListByAblitiy = response.data.data
      } catch (er) {
        console.error(er)
        return
      }
    }
  },

  mounted() {}
}
</script>

<style lang="scss">
.container {
  height: 100vh;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.errorInfo {
  position: absolute;
  right: 50px;
  top: 50px;
  background-color: #f5f8f9;
  border: 1px solid #c0bfbc;
  border-radius: 8px;
  padding: 12px;
}
</style>
