<template>
  <div class="py-8 flex flex-col gap-3">
    (debug) Daya in component 2:{{ carriers }}
    <div class="flex gap-3">
      <button class="bg-green-500 p-4 rounded" @click="addCarrier">ADD</button>
      <button class="bg-red-500 p-4 rounded" @click="deleteAll">
        DELETE ALL
      </button>
    </div>
    <div
      v-for="carrier in carriers"
      :key="carrier.id"
      class="bg-amber-300 flex gap-4 items-center p-4"
    >
      Name: {{ carrier.name }}
      <button class="bg-red-500 p-2 rounded" @click="deleteEntry(carrier.id)">
        DELETE
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Carrier } from "~/models/Carrier";

interface comp1Props {
  carriers: Carrier[];
}

const { carriers } = defineProps<comp1Props>();

const emit = defineEmits(["addEntry", "deleteEntry", "deleteAll"]);

// -----------------------------------
// logMessage
// --------------------------------------
function logMessage() {
  console.log(
    "DATA IN COMP2:",
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
function addCarrier() {
  const newId = carriers[carriers.length - 1].id + 1;

  emit("addEntry", { id: newId, name: generateRandomName() });
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

// -------------------------------------------------------
// getRandomInt
// -------------------------------------------------------
function getRandomInt(min: number, max: number): number {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

// -------------------------------------------------------
// generateRandomName
// -------------------------------------------------------
function generateRandomName(): string {
  const firstNames = [
    "John",
    "Jane",
    "Alice",
    "Bob",
    "Charlie",
    "Dana",
    "Eve",
    "Frank",
    "Grace",
    "Hank",
  ];
  const randomFirstName = firstNames[getRandomInt(0, firstNames.length - 1)];
  return randomFirstName;
}
</script>

<style></style>
