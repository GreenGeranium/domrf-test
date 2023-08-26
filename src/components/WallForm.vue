<template>
  <form class="wall-form">
    <h2>Стена</h2>
    <label>
      Введите ширину стены:
      <input type="number" @input="heightInput" /> см
    </label>
    <label>
      Введите высоту стены:
      <input type="number" @input="widthInput" /> см
    </label>
  </form>
</template>

<script>
export default {
  name: "WallForm",
  data() {
    return {
      wallHeight: 0,
      wallWidth: 0,
    };
  },
  methods: {
    heightInput(event) {
      this.$data.wallHeight = event.target.value;
    },
    widthInput(event) {
      this.$data.wallWidth = event.target.value;
    },
  },
};
</script>
