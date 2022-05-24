<template>
  <button v-show="!showModal" @click="showModal = true">
    Add new movement
  </button>
  <teleport to="#app">
    <ModalComp v-show="showModal" @close="showModal = false">
      <form @submit.prevent="submit">
        <div class="field">
          <label>Title*</label>
          <input required type="text" v-model="title" />
        </div>
        <div class="field">
          <label>Amount*</label>
          <input required type="number" v-model="amount" />
        </div>
        <div class="field">
          <label>Description</label>
          <textarea rows="4" v-model="description" />
        </div>
        <div class="field">
          <label class="radio-label">
            <input type="radio" v-model="movementType" value="Income" />
            <span>Income</span>
          </label>
          <label class="radio-label">
            <input type="radio" v-model="movementType" value="Expence" />
            <span>Expence</span>
          </label>
        </div>
        <div class="action">
          <button>Add movement</button>
        </div>
      </form>
    </ModalComp>
  </teleport>
</template>

<script setup>
import { ref, defineEmits } from "vue";
import ModalComp from "./ModalComp.vue";

const showModal = ref(false);
const title = ref("");
const amount = ref(null);
const description = ref("");
const movementType = ref("Income");
const emit = defineEmits(["create"]);

const submit = () => {
  showModal.value = !showModal.value;
  emit("create", {
    title: title.value,
    description: description.value,
    amount: movementType.value === "Income" ? amount.value : -amount.value,
    time: new Date(),
    id: new Date(),
  });
  title.value = "";
  description.value = "";
  amount.value = null;
  movementType.value = "Income";
};
</script>

<style scoped>
button {
  color: white;
  font-size: 1.12rem;
  background-color: var(--brand-blue);
  border: none;
  width: 100%;
  padding: 22px 28px;
  border-radius: 30px;
  box-sizing: border-box;
}
form {
  font-size: 1.24rem;
  width: 100%;
}
form .action {
  padding: 0 24px;
}
.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}
label {
  margin-bottom: 8px;
}
input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--brand-blue);
  border-radius: 8px;
  padding: 8px;
}
input[type="number"] {
  text-align: right;
}
.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}
.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}
input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: var(--brand-blue);
  border: 2px solid var(--brand-blue);
  border-radius: 50%;
}
input[type="radio"]:checked {
  background-color: var(--brand-blue);
}
</style>
