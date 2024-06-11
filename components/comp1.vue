<template>
  <div class="py-8">
    (debug) Data in component 1: {{ carriers }}
    <comp2
      :carriers="carriers"
      @add-entry="(newEntry) => addCarrier(newEntry)"
      @delete-entry="(id) => deleteEntry(id)"
      @delete-all="deleteAll"
    />
  </div>
</template>

<script setup lang="ts">
import type { Carrier } from "~/models/Carrier";
import comp2 from "./comp2.vue";

interface comp1Props {
  carriers: Carrier[];
}

const { carriers } = defineProps<comp1Props>();

const emit = defineEmits(["addEntry", "deleteEntry", "deleteAll"]);

// --------------------------------------
// logMessage
// --------------------------------------
function logMessage() {
  console.log(
    "DATA IN COMP1:",
    carriers.map((carrier) => carrier.name)
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
  emit("addEntry", newEntry);
}

// -------------------------------------------------------
// deleteEntry
// -------------------------------------------------------
function deleteEntry(id: number) {
  emit("deleteEntry", id);
}

// -------------------------------------------------------
// deleteAll
// -------------------------------------------------------
function deleteAll() {
  emit("deleteAll");
}
</script>

<style></style>
