<template>
  <LayoutComp>
    <template #header>
      <HeaderComp />
    </template>
    <template #resume>
      <ResumeComp
        :total-label="'Ahorro total'"
        :label="label"
        :total-amount="totalAmount"
        :amount="amount"
      >
        <template #graphic>
          <GraphicComp :amounts="amounts" />
        </template>
        <template #action>
          <ActionComp @create="create" />
        </template>
      </ResumeComp>
    </template>
    <template #movements>
      <MovementsComp @remove="remove" :movements="movements" />
    </template>
  </LayoutComp>
</template>

<script>
import LayoutComp from "./LayoutComp.vue";
import HeaderComp from "./HeaderComp.vue";
import ResumeComp from "./Resume/IndexComp.vue";
import ActionComp from "./ActionComp.vue";
import MovementsComp from "./Movements/IndexComp.vue";
import GraphicComp from "./Resume/GraphicComp.vue";

export default {
  components: {
    LayoutComp,
    HeaderComp,
    ResumeComp,
    ActionComp,
    MovementsComp,
    GraphicComp,
  },
  data() {
    return {
      label: null,
      amount: null,
      movements: [],
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movements
        .filter((m) => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);
          return m.time > oldDate;
        })
        .map((m) => m.amount);

      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);
        return lastMovements.reduce((suma, movement) => {
          return suma + movement;
        }, 0);
      });
    },
    totalAmount() {
      return this.movements.reduce((suma, m) => {
        return suma + m.amount;
      }, 0);
    },
  },
  mounted() {
    const movements = JSON.parse(localStorage.getItem("movements"));

    if (Array.isArray(movements)) {
      this.movements = movements.map((m) => {
        return { ...m, time: new Date(m.time) };
      });
    }
  },
  methods: {
    create(movement) {
      this.movements.push(movement);
      this.save();
    },
    remove(id) {
      const index = this.movements.findIndex((m) => m.id === id);
      this.movements.splice(index, 1);
      this.save();
    },
    save() {
      localStorage.setItem("movements", JSON.stringify(this.movements));
    },
  },
};
</script>
