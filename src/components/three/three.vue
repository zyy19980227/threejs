<template>
  <div class="wrapper">
    <div id="three-container"></div>
    <div id="instructions">click and drag to control the animation</div>
  </div>
</template>

<script>
export default {
  props: ["imgurl", "size"],
  data() {
    return {
      url: [this.imgurl.img1, this.imgurl.img2],
    };
  },
  mounted() {
    this.init(this.url);
  },
  methods: {
    init(arr) {
      let root = new THREERoot({
        createCameraControls: !true,
        antialias: window.devicePixelRatio === 1,
        fov: 80,
      });
      root.renderer.setClearColor(0x000000, 0);
      root.renderer.setPixelRatio(window.devicePixelRatio || 1);
      root.camera.position.set(0, 0, 60);

      let slide = new Slide(this.size.width, this.size.height, "out");
      let l1 = new THREE.ImageLoader();
      l1.setCrossOrigin("Anonymous");
      l1.load(arr[0], function (img) {
        slide.setImage(img);
      });
      root.scene.add(slide);

      let slide2 = new Slide(this.size.width, this.size.height, "in");
      let l2 = new THREE.ImageLoader();
      l2.setCrossOrigin("Anonymous");
      l2.load(arr[1], function (img) {
        slide2.setImage(img);
      });
      root.scene.add(slide2);
      let tl = new TimelineMax({ repeat: -1, repeatDelay: 1.0, yoyo: true });
      tl.add(slide.transition(), 0);
      tl.add(slide2.transition(), 0);
      createTweenScrubber(tl);
    },
  },
};
</script>

<style scoped>
body {
  margin: 0;
  overflow: hidden;
}

canvas {
  background-image: radial-gradient(#666, #333);
}

#instructions {
  position: absolute;
  color: #fff;
  bottom: 0;
  padding-bottom: 6px;
  font-family: sans-serif;
  width: 100%;
  text-align: center;
  pointer-events: none;
}
</style>