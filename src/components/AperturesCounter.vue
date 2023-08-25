<template>
  <div class="apertures">
    <h2>Проёмы</h2>
    <h3>Количество проёмов: {{ apertures.length }}</h3>
    <ul>
      <li v-for="(aperture, index) in apertures" :key="index">
        <form>
          <label>Ширина<input type="number" /> см</label>
          <label>Высота<input type="number" /> см</label>
          <button @click="deleteAperture($event, index)">Удалить</button>
        </form>
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
      this.apertures.push({
        id: this.apertures.length + 1,
        height: 0,
        width: 0,
      });
      console.log(this.apertures);
    },
    deleteAperture(event, id) {
      event.preventDefault();
      this.apertures.splice(id, 1);
      console.log(this.apertures);
    },
  },
};
</script>
