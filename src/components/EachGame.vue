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
      <p>Genre: {{item.genre}}</p>
      <p>Developed by: {{item.developer}}</p>
      <p>Release date: {{item.release}}</p>
      <button @click= "rateGame">Rate the game</button>
      <div>
        <h3>Total score</h3>
        <p>{{totalScore}}</p>
      </div>
      
    </div>
    <div v-show ="toggleRate">
      <h3>Rate the game</h3>
      <p>Graphics</p>
      <input type="number" v-model ="graphicsScore" name="graphics__score" min="0" max="20">
      <p>Sound</p>
      <input type="number" name="sound__score" min="0" max="15">
      <p>Gameplay</p>
      <input type="number" name="gameplay__score" min="0" max="30">
      <p>Feeling</p>
      <input type="number" name="feeling__score" min="0" max="20">
      <p>Storyline</p>
      <input type="number" name="storyline__score" min="0" max="5">
      <p>General impression</p>
      <input type="number" name="impression__score" min="0" max="10">
    </div>
  </div>
</template>

<script>
export default {
  name: "EachGame",
  props: ["item"],
  data() {
    return {
      toggleRate: false,
      detailsState: false,
      totalScore: null,
      graphicsScore: null,
      soundScore: null,
      gameplayScore: null,
      feelingScore: null,
      storylineScore:null,
      impressionScore:null,
    }
  },
  methods: {
    toggleDetails() {
      this.detailsState = !this.detailsState
    },
    rateGame(){
      this.toggleRate =!this.toggleRate
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
