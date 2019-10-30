<template>
  <div class="games-list">
    <div class="games-list__form">
      <label for="name">Name of the game</label>
      <input
        v-model="newGame.name"
        id="name"
      />
      <label for="game_genre">Select game's genre</label>
      <select
        v-model="newGame.genre"
        id="game_genre"
        name="genres"
      >
        <option value disabled selected>Select genre...</option>
        <option value="Real Time Strategy">Real Time Strategy</option>
        <option value="Role Playing Game">Role Playing Game</option>
        <option value="Turn Based Strategy">Turn Based Strategy</option>
        <option value="First Person Shooter">First Person Shooter</option>
        <option value="Action & Adventure">Action & adventure</option>
        <option value="Sports & Racing">Sports & Racing</option>
      </select>
      <label for="release_date">Release date</label>
      <input
        v-model="newGame.release"
        id="release_date"
      />
      <label for="developer">Developer's name</label>
      <input
        v-model="newGame.developer"
        id="developer"
      />
      <label for="game_image">Upload an image</label>
      <input
        type="file"
        accept="image/*"
        @change="uploadImage($event)"
        id="game_image"
        ref="fileInput"
      />
      <button @click="addGame">Add game</button>
    </div>
    <EachGame
      v-for="item in games"
      :item="item"
      :key="item.name"
    />
  </div>
</template>

<script>
import EachGame from "./EachGame.vue"
export default {
  name: "GamesList",
  components: {
    EachGame
  },
  data() {
    return {
      newGame: {
        name: null,
        genre: null,
        release: null,
        developer: null,
        image: null
      },
      games: [
        {
          name: "Metro: Exodus",
          genre: "FPS",
          release: 2019,
          developer: "4A Games",
          image: "images/metroExodus.jpg"
        },
        {
          name: "Dishonored 2",
          genre: "Action/Stealth",
          release: 2016,
          developer: "Arkane Studios",
          image: "images/dishonored2.jpg"
        }
      ]
    }
  },
  computed: {
    isDuplicate() {
      return this.games.some(item => {
        return item.name.toLowerCase() === this.newGame.name.toLowerCase()
      })
    }
  },
  methods: {
    addGame() {
      if (this.newGame.name != null && this.newGame.genre != null && this.newGame.release != null && this.newGame.developer != null) {
        if(!this.isDuplicate ){
          this.games.push(this.newGame)
          this.newGame = {}
          this.$refs.fileInput.value = ""
        } else {
          alert("There is already a game with that name in the library")
        }
       
      } else {
        alert("Please fill all the inputs")
      }
      
    },
    uploadImage(e) {
      const image = e.target.files[0]
      const reader = new FileReader()
      reader.readAsDataURL(image)
      reader.onload = e => {
        this.newGame.image = e.target.result
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.games-list__form {
  display: grid;
  grid-template-columns: auto auto;
}
</style>
