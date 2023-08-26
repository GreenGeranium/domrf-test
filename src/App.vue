<template>
  <h1>Калькулятор ПГП</h1>
  <SlabsCalculatorForm />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import SlabsCalculatorForm from "./components/SlabsCalculatorForm.vue";

export default defineComponent({
  name: "App",
  components: { SlabsCalculatorForm },
});
</script>
