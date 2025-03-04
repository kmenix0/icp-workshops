<script setup>
import { ref, onMounted } from "vue";
import { my_project_backend } from "declarations/my_project_backend/index";

let a = ref(null);
let b = ref(null);
let operator = ref("+");
let result = ref("");

async function handleCalculate(e) {
  e.preventDefault();
  if (a.value === null || b.value === null) {
    result.value = "Please enter both numbers.";
    return;
  }

  try {
    const response = await my_project_backend.calculate(a.value, b.value, operator.value);
    result.value = response;
    localStorage.setItem("lastResult", response);
  } catch (error) {
    result.value = "Error occurred: " + error.message;
  }
}

onMounted(() => {
  const storedResult = localStorage.getItem("lastResult");
  if (storedResult) {
    result.value = storedResult;
  }
});
</script>

<template>
  <form
    action="#"
    @submit="handleCalculate"
    class="flex flex-col items-center justify-center gap-4 p-10 border-2 rounded-lg border-violet-950"
  >
    <label for="a" class="text-xl font-light text-violet-50">Enter number A:</label>
    <input
      id="a"
      v-model.number="a"
      type="number"
      placeholder="Number A"
      class="text-center text-black rounded-lg outline-violet-950"
    />
    <label for="b" class="text-xl font-light text-violet-50">Enter number B:</label>
    <input
      id="b"
      v-model.number="b"
      type="number"
      placeholder="Number B"
      class="text-center text-black rounded-lg outline-violet-950"
    />
    <label for="operator" class="text-xl font-light text-violet-50">Select an operator:</label>
    <select id="operator" v-model="operator" class="text-center text-black rounded-lg outline-violet-950">
      <option value="+">+</option>
      <option value="-">-</option>
      <option value="*">*</option>
      <option value="/">/</option>
      <option value="%">%</option>
    </select>
    <button
      type="submit"
      class="p-2 font-semibold rounded-lg bg-gradient-to-r from-violet-800 to-violet-950 text-violet-50"
    >
      Calculate
    </button>
    <p class="text-xl font-light text-center w-fit text-violet-50">{{ result }}</p>
  </form>
</template>