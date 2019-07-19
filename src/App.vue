<template>
  <div id="app">
    <HelloWorld :images="image" @next="nextImage" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld
  },
  data() {
    return {
      imageArray: [
        "https://picsum.photos/id/334/250/200",
        "https://picsum.photos/id/225/250/200"
      ],
      index: 0
    };
  },
  computed: {
    image: function() {
      // return [this.imageArray[this.index]];
      // comment below line and line no 63 and uncomment in /components/HelloWorld.vue to Use custom next functionality
      return this.imageArray;
    }
  },
  methods: {
    nextImage() {
      this.index = this.index === 1 ? 0 : 1;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}
</style>
