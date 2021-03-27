<template>
  <div id="app">
    <three :imgurl="imgurl" :size="size"></three>
    <router-view />
  </div>
</template>

<script>
import three from "./components/three/three";
export default {
  name: "App",
  components: {
    three
  },
  data() {
    return {
      imgurl: {
        img1: require("../static/spring.jpg"),
        img2: require("../static/winter.jpg"),
        img3: require("../static/bg2.jpg")
      },
      size: {
        width: 100,
        height: 60
      }
    };
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
</style>
