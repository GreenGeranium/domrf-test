<template>
  <div>
    <p>Количество ПГП: {{ blocksAmount }}</p>
    <p>Общий вес стены: {{ totalWallWeight }} кг</p>
  </div>
</template>
<script>
export default {
  props: ["blocksAmount"],
  name: "ResultsSection",
  computed: {
    totalWallWeight() {
      return this.blocksAmount * 36;
    },
  },
};
</script>
