<template>
  <h1>Калькулятор ПГП</h1>
  <WallForm></WallForm>
  <AperturesCounter></AperturesCounter>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import WallForm from "./components/WallForm.vue";
import AperturesCounter from "./components/AperturesCounter.vue";

export default defineComponent({
  name: "App",
  components: {
    WallForm,
    AperturesCounter,
  },
});
</script>
