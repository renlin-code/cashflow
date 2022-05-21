<template>
  <LayoutComp>
    <template #header>
      <HeaderComp />
    </template>
    <template #resume>
      <ResumeComp
        :total-label="'Ahorro total'"
        :label="label"
        :total-amount="1000"
        :amount="amount"
      >
        <template #graphic> graphic </template>
        <template #action> action </template>
      </ResumeComp>
    </template>
    <template #movements>
      <MovementsComp />
    </template>
  </LayoutComp>
</template>

<script>
import LayoutComp from "./LayoutComp.vue";
import HeaderComp from "./HeaderComp.vue";
import ResumeComp from "./Resume/IndexComp.vue";
import MovementsComp from "./Movements/IndexComp.vue";
export default {
  components: {
    LayoutComp,
    HeaderComp,
    ResumeComp,
    MovementsComp,
  },
  data() {
    return {
      label: null,
      amount: null,
    };
  },
};
</script>
