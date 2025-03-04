<template>
  <div class="flex flex-col items-center justify-center gap-4 p-10">
    <ICP />
    <Calculator />
  </div>
</template>

<script>
import ICP from "./components/Icp.vue";
import Calculator from "./components/Calculator.vue";

export default {
  components: {
    ICP,
    Calculator,
  },
};
</script>