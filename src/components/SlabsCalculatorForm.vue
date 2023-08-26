<template>
  <form @submit.prevent="onSubmit">
    <WallForm
      wallHeight="wallHeight"
      wallWidth="wallWidth"
      @updateWallParams="updateWallParams"
    ></WallForm>
    <div class="apertures">
      <h2>Проёмы</h2>
      <h3>Количество проёмов: {{ apertures.length }}</h3>
      <ul>
        <li v-for="(aperture, index) in apertures" :key="aperture.id">
          <label
            >Ширина<input type="number" v-model="aperture.width" /> см</label
          >
          <label
            >Высота<input type="number" v-model="aperture.height" /> см</label
          >
          <button @click="deleteAperture(index)">Удалить</button>
        </li>
      </ul>
      <button type="button" @click="addAperture">Добавить проём</button>
    </div>
    <button type="submit">Считать</button>
    <p>{{ errorMessage }}</p>
    <ResultsSection :blocksAmount="blocksAmount"></ResultsSection>
  </form>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import WallForm from "@/components/WallForm.vue";
import ResultsSection from "@/components/ResultsSection.vue";

interface Aperture {
  id: number;
  height: number;
  width: number;
}

export default defineComponent({
  name: "SlabsCalculatorForm",
  components: { WallForm, ResultsSection },

  data() {
    return {
      wallHeight: 0,
      apertures: [] as Aperture[],
      idCounter: 1,
      wallWidth: 0,
      idAperturesCounter: 1,
      wallArea: 0,
      aperturesArea: 0,
      blocksAmount: 0,
      errorMessage: "",
    };
  },
  methods: {
    onSubmit() {
      if (this.wallHeight === 0 || this.wallWidth === 0) {
        this.errorMessage = "Данные введены некорректно";
        return;
      }
      this.errorMessage = "";
      this.wallArea = this.wallWidth * this.wallHeight;
      this.apertures.map((aperture) => {
        this.aperturesArea += aperture.width * aperture.height;
      });
      this.blocksAmount = Math.ceil(
        (this.wallArea - this.aperturesArea) / (66.7 * 50)
      );
      console.log(this.blocksAmount);
    },
    updateWallParams(newWallWidth: number, newWallHeight: number) {
      this.wallWidth = newWallWidth;
      this.wallHeight = newWallHeight;
    },
    addAperture() {
      this.apertures.push({
        id: this.idCounter++,
        height: 0,
        width: 0,
      });
    },
    deleteAperture(index: number) {
      this.apertures.splice(index, 1);
    },
  },
});
</script>
