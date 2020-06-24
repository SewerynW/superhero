<template>
  <section>
    <header>
      <h1>Superheros</h1>
    </header>

    <main>
      <ul v-if="superheroList.length > 0">
        <li class="hero" v-for="(hero, idx) in superheroList" :key="idx">
          <img
            :src="hero.avatarURL"
            alt="Avatar"
            @error="showError"
            onerror="this.src='https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcQmm3b5D-piofm2LtGv5BklaY1L_UbydLJJ6Q&usqp=CAU';"
          />
          <div>
            <p class="hero--nickname">{{ hero.nombre }}</p>
            <p class="hero--real-name">{{ hero.nombreReal }}</p>
          </div>
        </li>
      </ul>
      <div class="empty-info" v-if="superheroList.length === 0">
        None of Superhero Match.
      </div>
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
  methods: {
    showError() {
      this.$emit('showBox')
    }
  }
}
</script>

<style lang="scss" scoped>
section {
  width: 400px;
  min-height: 300px;
}
.empty-info {
  text-align: center;
  padding: 12px;
  width: 100%;
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
