<template>
  <div>
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
  },
  name: "ResultsSection",
  computed: {
    totalWallWeight(): number {
      return (this.blocksAmount ?? 0) * 36;
    },
  },
});
</script>
