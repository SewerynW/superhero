<template>
  <section>
    <header>
      <h1>Find your hero</h1>
    </header>
    <main>
      <p>Filter By Superhero ID</p>
      <input id="heroId" type="number" v-model="heroId" name="heroId" />

      <p>Filter By Abilities to fly</p>

      <input
        type="radio"
        name="ability"
        id="canFly"
        value="canFly"
        v-model="heroAbility"
      />
      <label for="canFly">Can Fly</label>
      <br />

      <input
        type="radio"
        name="ability"
        id="canNotFly"
        value="canNotFly"
        v-model="heroAbility"
      />
      <label for="canFly">Can't Fly</label>
      <br />

      <input
        type="radio"
        name="ability"
        id="all"
        value="all"
        v-model="heroAbility"
      />
      <label for="All">All</label>
      <br />

      <p>Filter By Superhero Nickname</p>
      <input
        type="text"
        name="heroNickname"
        id="heroNickname"
        v-model="heroNickname"
      />
    </main>
  </section>
</template>

<script>
export default {
  name: 'Panel',
  data() {
    return {
      heroId: null,
      heroAbility: '',
      heroNickname: ''
    }
  },

  watch: {
    heroId(value) {
      this.$emit('enteredId', Number(value))
    },

    heroAbility(value) {
      this.$emit('pickedAbility', value)
    },

    heroNickname(value) {
      this.$emit('entereNickname', value)
    }
  }
}
</script>

<style lang="scss" scoped>
section {
  width: 300px;
  min-height: 300px;
}

h1 {
  text-align: center;
}

main {
  padding: 12px;

  p {
    padding: 28px 0px 6px;

    &:first-child {
      padding-top: 0px;
    }
  }
}
</style>
