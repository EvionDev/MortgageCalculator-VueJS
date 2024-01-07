<template>
  <div class="h-1/2 w-full rounded-lg border-8 border-white p-10">
    <h1 class="text-xl font-semibold">Mortgage calculator</h1>
    <div class="mt-5 grid auto-rows-auto grid-cols-2 gap-8 md:grid-cols-3">
      <div class="flex flex-col gap-1">
        <h3>
          Purchase price:
          <span class="font-semibold">${{ purchasePrice }}</span>
        </h3>
        <input
          type="range"
          class="accent-[#AF89FF]"
          v-model="purchasePrice"
          min="0"
          step="5000"
          max="3000000"
          value="0"
        />
      </div>
      <div class="flex flex-col gap-1">
        <h3>
          Down payment: <span class="font-semibold">${{ downPayment }}</span>
        </h3>
        <input
          type="range"
          class="accent-[#AF89FF]"
          v-model="downPayment"
          min="0"
          step="5000"
          max="700000"
          value="0"
        />
      </div>
      <div class="flex flex-col gap-1">
        <h3>
          Repayment time:
          <span class="font-semibold">{{ repaymentTime }}</span> years
        </h3>
        <input
          type="range"
          class="accent-[#AF89FF]"
          v-model="repaymentTime"
          min="0"
          max="30"
          value="0"
        />
      </div>
      <div class="flex flex-col gap-1">
        <h3>
          Interest rate: <span class="font-semibold">{{ interestRate }}%</span>
        </h3>
        <input
          type="range"
          class="accent-[#AF89FF]"
          v-model="interestRate"
          min="0"
          max="25"
          value="0"
        />
      </div>
      <div class="flex flex-col gap-1">
        <h3>Loan amount:</h3>
        <h1>
          <span class="font-semibold">${{ loanAmount }}</span>
        </h1>
      </div>
      <div class="flex flex-col gap-1">
        <h3>Estimated pr. month:</h3>
        <h1>
          <span class="font-semibold">${{ estimatedMonth }}</span>
        </h1>
      </div>

      <button
        class="rounded-md bg-[#8C56FF] py-4 text-white"
        @click="computeMortgage"
      >
        Get a quote
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const purchasePrice = ref(0);
const downPayment = ref(0);
const repaymentTime = ref(0);
const interestRate = ref(0);
const loanAmount = ref(0);
const estimatedMonth = ref(0);

const computeMortgage = () => {
  const interest = interestRate.value / 100 / 12;
  const repayment = repaymentTime.value * 12;

  const dividend = ((1 + interest) ** repayment).toFixed(4);

  const divisor = ((1 + interest) ** repayment - 1).toFixed(4);

  loanAmount.value = purchasePrice.value - downPayment.value;

  estimatedMonth.value = (
    loanAmount.value *
    interest *
    (dividend / divisor)
  ).toFixed(2);
};
</script>

<style scoped></style>
