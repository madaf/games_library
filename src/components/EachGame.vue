<template>
  <div class="game">
    <img
      :src="item.image"
      class="game__image"
    />
    <h2>{{item.name}}</h2>
    <button @click="toggleDetails">View details</button>
    <div
      v-show="detailsState"
      class="game__details"
    >
      <h2>{{item.name}}</h2>
      <p>{{item.genre}}</p>
      <p>{{item.developer}}</p>
      <p>{{item.release}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "EachGame",
  props: ["item"],
  data() {
    return {
      detailsState: false
    }
  },
  methods: {
    toggleDetails() {
      this.detailsState = !this.detailsState
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.game__image {
  width: 145px;
  height: 200px;
}
</style>
