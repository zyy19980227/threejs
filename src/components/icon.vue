<template>
  <div class="imgbox" :style="style">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: ["imgData"],
  data() {
    return {
      style: {
        transform: `scale(${this.imgData.scale})`,
        transformOrigin: "0 0",
      },
    };
  },
};
</script>

<style scoped>
.imgbox {
  width: 100px;
  height: 100px;
  box-shadow: 18px 18px 30px rgba(0, 0, 0, 0.1),
    -18px -18px 30px rgba(255, 255, 255, 1);
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #efeeee;
  transition: box-shadow 0.2s ease-out;
}

.imgbox :first-child {
  transition: all 0.2s ease-out;
}
.imgbox:hover {
  box-shadow: 0px 0px 0px rgba(0, 0, 0, 0.2),
    0px 0px 0px rgba(255, 255, 255, 0.8),
    inset 18px 18px 30px rgba(0, 0, 0, 0.1),
    inset -18px -18px 30px rgba(255, 255, 255, 1);
  transition: box-shadow 0.2s ease-out;
}
.imgbox:hover :first-child {
  transform: scale(0.95);
  transition: all 0.2s ease-out;
}
</style>
