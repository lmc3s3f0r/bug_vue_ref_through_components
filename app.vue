<template>
  <div class="p-4">
    (debug) Data in App: {{ carriersData }}
    <comp1
      :carriers="carriersData"
      @add-entry="(newEntry) => addCarrier(newEntry)"
      @delete-entry="(id) => deleteEntry(id)"
      @delete-all="deleteAll"
    />
  </div>
</template>

<script setup lang="ts">
import { carriers } from "./assets/carriersData";
import comp1 from "./components/comp1.vue";
import type { Carrier } from "./models/Carrier";

const carriersData = ref<Carrier[]>([]);
carriersData.value = carriers;

const originalCarriersData = ref<Carrier[]>([]);
originalCarriersData.value = carriers;

// --------------------------------------
// logMessage
// --------------------------------------
function logMessage() {
  console.log(
    "DATA IN APP:",
    carriersData.value.map((carrier) => carrier.name)
  );
}

// --------------------------------------
// onMounted
// --------------------------------------
onMounted(() => {
  setInterval(logMessage, 3000);
});

// -------------------------------------------------------
// addCarrier
// -------------------------------------------------------
function addCarrier(newEntry: Carrier) {
  carriersData.value.push(newEntry);
}

// -------------------------------------------------------
// deleteEntry
// -------------------------------------------------------
function deleteEntry(id: number) {
  carriersData.value = carriersData.value.filter(
    (carrier: Carrier) => carrier.id !== id
  );
}

// -------------------------------------------------------
// deleteAll
// -------------------------------------------------------
function deleteAll() {
  carriersData.value = [];
}
</script>
