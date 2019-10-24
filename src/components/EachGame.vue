<template>
  <div class="hello">
    <img id="cover" :src="item.image" />
    <h2>{{item.name}}</h2>
    <button @click="toggleDetails">View details</button>
    <div v-show="detailsState">
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
    };
  },
  methods: {
    toggleDetails() {
      this.detailsState = !this.detailsState;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#cover {
  width: 145px;
  height: 200px;
}
</style>
