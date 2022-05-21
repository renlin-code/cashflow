<template>
  <Suspense>
    <template #default>
      <HomeComp />
    </template>
    <template #fallback>
      <SplashScreenComp />
    </template>
  </Suspense>
</template>

<script>
import SplashScreenComp from "./components/SplashScreenComp.vue";
import { defineAsyncComponent } from "vue";

export default {
  components: {
    SplashScreenComp,
    HomeComp: defineAsyncComponent(
      () =>
        new Promise((resolve) => {
          setTimeout(() => {
            resolve(import("./components/HomeComp.vue"));
          }, 2500);
        })
    ),
  },
};
</script>

<style>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}

:root {
  --brand-green: #04b500;
  --brand-blue: #0689b0;
}
</style>
