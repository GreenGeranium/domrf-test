<template>
  <div class="page">
    <h1>Калькулятор ПГП</h1>
    <SlabsCalculatorForm />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import SlabsCalculatorForm from "./components/SlabsCalculatorForm.vue";

export default defineComponent({
  name: "App",
  components: { SlabsCalculatorForm },
});
</script>

<style lang="scss">
.root {
  margin: 0;
}
.page {
  margin: 0 auto;
  font-family: "Montserrat", Arial, sans-serif;
  display: flex;
  flex-direction: column;

  h1 {
    margin: 30px auto;
    font-size: 48px;
    font-weight: 900;
  }
}
</style>
