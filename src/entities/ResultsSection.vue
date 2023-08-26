<template>
  <div v-if="areResultsVisible" class="results">
    <p>Количество ПГП: {{ blocksAmount }}</p>
    <p>Общий вес стены: {{ totalWallWeight }} кг</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    blocksAmount: {
      type: Number,
    },
    areResultsVisible: Boolean,
  },
  name: "ResultsSection",
  computed: {
    totalWallWeight(): number {
      return (this.blocksAmount ?? 0) * 36;
    },
  },
});
</script>

<style>
.results {
  background-color: #a52a2a29;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 auto;
  grid-area: results;
  padding: 0px 75px;
  border: 2px beige solid;
  border-radius: 25px;
}
</style>
