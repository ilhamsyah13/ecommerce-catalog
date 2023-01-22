<script setup>
import ProductDisplay from "./components/ProductDisplay.vue";
</script>

<template>
  <main>
    <Suspense>
      <template #default>
        <ProductDisplay />
      </template>
      <template #fallback>
        <div class="loader"></div>
      </template>
    </Suspense>
  </main>
</template>

<style scoped>
.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #3498db; /* Blue */
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
