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
        <template #action>
          <ActionComp />
        </template>
      </ResumeComp>
    </template>
    <template #movements>
      <MovementsComp :movements="movements" />
    </template>
  </LayoutComp>
</template>

<script>
import LayoutComp from "./LayoutComp.vue";
import HeaderComp from "./HeaderComp.vue";
import ResumeComp from "./Resume/IndexComp.vue";
import ActionComp from "./ActionComp.vue";
import MovementsComp from "./Movements/IndexComp.vue";
export default {
  components: {
    LayoutComp,
    HeaderComp,
    ResumeComp,
    ActionComp,
    MovementsComp,
  },
  data() {
    return {
      label: null,
      amount: null,
      movements: [
        {
          id: 0,
          title: "Movimiento 1",
          description: "Lorem ipsum dolor sit amen",
          amount: 300,
        },
        {
          id: 1,
          title: "Movimiento 2",
          description: "Lorem ipsum dolor sit amen",
          amount: -100,
        },
        {
          id: 2,
          title: "Movimiento 3",
          description: "Lorem ipsum dolor sit amen",
          amount: 320,
        },
        {
          id: 3,
          title: "Movimiento 4",
          description: "Lorem ipsum dolor sit amen",
          amount: -150,
        },
      ],
    };
  },
};
</script>
