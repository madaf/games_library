<template>
  <div class="games-list">
    <div class="games-list__form">
      <input
        v-model="newGame.name"
        placeholder="Name..."
      />
      <select
        v-model="newGame.genre"
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
      <input
        v-model="newGame.release"
        placeholder="Release date..."
      />
      <input
        v-model="newGame.developer"
        placeholder="Developer..."
      />
      <input
        type="file"
        accept="image/*"
        @change="uploadImage($event)"
        id="file-input"
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
        name: "",
        genre: "",
        release: null,
        developer: "",
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
      if (!this.isDuplicate) {
        this.games.push(this.newGame)
      }
      this.newGame = {}
      this.$refs.fileInput.value = ""
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
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
