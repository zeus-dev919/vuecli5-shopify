<template>
  <select v-model='flightType'>
    <option value="one-way flight">One-way Flight</option>
    <option value="return flight">Return Flight</option>
  </select>

  <input type="date" v-model='departureDate'>
  <input type= "date" v-model='returnDate' :disabled="!isReturn">
  <button :disabled="!canBook" @click="book">book</button>

</template>

<script setup>
import { ref, computed } from 'vue';
const flightType = ref('one-way flight');
const departureDate = ref(new Date());
const returnDate = ref(departureDate.value);
const isReturn = computed(() => flightType.value === 'return flight')

const canBook = computed(() =>
  !isReturn.value || returnDate.value > departureDate.value)

function book() {
  alert(isReturn.value ? 'booked' : 'one way')
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
select,
input,
button {
  display: block;
  margin: 0.5em 0;
  font-size: 15px;
}

input[disabled] {
  color: #999;
}

p {
  color: red;
}
</style>