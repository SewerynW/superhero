<template>
  <section>
    <header>
      <h1>Superheros</h1>
    </header>

    <main>
      <ul>
        <li class="hero" v-for="(hero, idx) in superheroList" :key="idx">
          <img :src="hero.avatarURL" alt="Avatar" />
          <div>
            <p class="hero--nickname">{{ hero.nombre }}</p>
            <p class="hero--real-name">{{ hero.nombreReal }}</p>
          </div>
        </li>
      </ul>
    </main>
  </section>
</template>

<script>
export default {
  name: 'List',
  props: {
    superheroList: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {}
  },
  watch: {
    superheroList(value) {
      console.log('i get list', value)
    }
  },
  mounted() {}
}
</script>

<style lang="scss" scoped>
section {
  width: 400px;
  min-height: 300px;
}

header {
  padding: 10px;
  background-color: #eaeae8;
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
  border-bottom: 1px solid #c0bfbc;

  h1 {
    font-size: 20px;
    font-weight: normal;
    letter-spacing: -1px;
  }
}

.hero {
  list-style: none;
  width: 100%;
  display: flex;
  padding: 6px 0px;
  border-top: 1px solid #c0bfbc;

  &:first-child {
    border-top: none;
  }

  img {
    vertical-align: middle;
    width: 60px;
    height: 60px;
    padding: 0px 50px;
    border-radius: 50%;
  }

  &--nickname {
    font-weight: bold;
    text-transform: capitalize;
  }

  &--real-name {
    font-size: 10px;
    padding-top: 6px;
  }
}
</style>
