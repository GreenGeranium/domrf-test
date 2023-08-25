<template>
  <div class="apertures">
    <h2>Проёмы</h2>
    <h3>Количество проёмов: {{ apertures.length }}</h3>
    <ul>
      <li v-for="(aperture, index) in apertures" :key="index">
        {{ (aperture, index) }}
      </li>
    </ul>
    <button @click="addAperture">Добавить проём</button>
  </div>
</template>

<script>
export default {
  name: "AperturesCounter",
  data() {
    return { apertures: [] };
  },
  methods: {
    addAperture() {
      this.apertures.push({});
      console.log(this.apertures);
    },
  },
};
</script>
