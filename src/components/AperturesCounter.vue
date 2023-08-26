<template>
  <div class="apertures">
    <h2>Проёмы</h2>
    <h3>Количество проёмов: {{ apertures.length }}</h3>
    <ul>
      <li v-for="(aperture, index) in apertures" :key="aperture.id">
        <label>Ширина<input type="number" v-model="aperture.width" /> см</label>
        <label
          >Высота<input type="number" v-model="aperture.height" /> см</label
        >
        <button @click="deleteAperture(index)">Удалить</button>
      </li>
    </ul>
    <button @click="addAperture">Добавить проём</button>
  </div>
</template>

<script>
export default {
  name: "AperturesCounter",
  data() {
    return { apertures: [], idCounter: 1 };
  },
  methods: {
    addAperture() {
      this.apertures.push({
        id: this.idCounter++,
        height: 0,
        width: 0,
      });
      console.log(this.apertures);
    },
    deleteAperture(index) {
      this.apertures.splice(index, 1);
      console.log(index);
    },
  },
};
</script>
