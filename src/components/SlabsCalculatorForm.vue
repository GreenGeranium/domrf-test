<template>
  <form @submit.prevent="onSubmit" class="calculator">
    <WallForm
      wallHeight="wallHeight"
      wallWidth="wallWidth"
      @updateWallParams="updateWallParams"
    ></WallForm>
    <div class="apertures">
      <h2>Проёмы для любых целей</h2>
      <h3>Количество проёмов: {{ apertures.length }}</h3>
      <ul>
        <li v-for="(aperture, index) in apertures" :key="aperture.id">
          <label
            >Ширина <input type="number" v-model="aperture.width" /> см</label
          >
          <label
            >Высота <input type="number" v-model="aperture.height" /> см</label
          >
          <button @click="deleteAperture(index)">Удалить</button>
        </li>
      </ul>
      <button type="button" @click="addAperture" class="add-button">
        Добавить проём
      </button>
    </div>
    <button class="submit-button" type="submit">Считать</button>
    <p class="error-message">{{ errorMessage }}</p>
    <ResultsSection
      :blocksAmount="blocksAmount"
      :areResultsVisible="areResultsVisible"
    ></ResultsSection>
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
      areResultsVisible: false,
    };
  },
  methods: {
    onSubmit() {
      if (this.wallHeight === 0 || this.wallWidth === 0) {
        this.errorMessage = "Данные введены некорректно";
        this.areResultsVisible = false;
        return;
      }
      this.areResultsVisible = true;
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

<style lang="scss">
input {
  width: 50px;
  border-radius: 9px;
}

.calculator {
  display: grid;
  flex-direction: column;
  margin: 0;
  padding: 0 100px;
  grid-auto-columns: 40% 60%;
  column-gap: 20px;
  grid-template-areas:
    "wall apertures"
    "submit submit"
    "error error"
    "results results";

  .add-button {
    margin: 0 auto 0;
    font-size: 15px;
    padding: 8px 32px;
    max-width: 190px;
    border-radius: 50px;
    border: none;
    width: 100%;
    cursor: pointer;
    background-color: #e76d16;
    color: white;

    &:hover {
      opacity: 0.9;
    }
  }

  .submit-button {
    margin: 30px auto 0;
    grid-area: submit;
    font-size: 25px;
    padding: 20px 40px;
    max-width: 235px;
    border-radius: 50px;
    border: none;
    width: 100%;
    cursor: pointer;
    background-color: #eb995f;
    color: white;

    &:hover {
      opacity: 0.9;
    }
  }

  .error-message {
    grid-area: error;
    margin: 20px auto 0;
    color: #ff4141;
    font-size: 20px;
    font-weight: 700;
  }

  .apertures {
    grid-area: apertures;
    display: flex;
    flex-direction: column;
    align-items: center;

    ul {
      margin: 0;
      padding: 0;

      li {
        list-style: none;
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 0 0 15px;
        row-gap: 5px;

        button {
          font-size: 12px;
          padding: 2px 0px;
          max-width: 100px;
          border-radius: 50px;
          border: none;
          width: 100%;
          cursor: pointer;
          background-color: #cb2b2b;
          color: white;
          margin: 0 auto 0;
        }
      }
    }

    h2 {
      margin: 0;
      font-weight: 600;
      font-size: 30px;
    }

    h3 {
      margin: 10px 0 10px;
      font-size: 20px;
    }
  }
}
</style>
