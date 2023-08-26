<template>
  <form class="wall-form">
    <h2>Стена</h2>
    <label>
      Введите ширину стены:
      <input type="number" v-model="localWallWidth" @input="emitUpdate" /> см
    </label>
    <label>
      Введите высоту стены:
      <input type="number" v-model="localWallHeight" @input="emitUpdate" /> см
    </label>
  </form>
</template>

<script>
export default {
  name: "WallForm",
  props: {
    wallHeight: Number,
    wallWidth: Number,
  },
  data() {
    return {
      localWallHeight: 0,
      localWallWidth: 0,
    };
  },
  methods: {
    emitUpdate() {
      this.$emit("updateWallParams", this.localWallWidth, this.localWallHeight);
    },
  },
};
</script>

<style lang="scss">
.wall-form {
  display: flex;
  flex-direction: column;
  row-gap: 30px;
  margin: 0;
  grid-area: wall;

  h2 {
    margin: 0;
    font-weight: 600;
    font-size: 30px;
  }
}
</style>
