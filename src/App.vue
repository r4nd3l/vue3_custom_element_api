<template>
  <main
    class="h-screen w-screen flex flex-col gap-10 items-center justify-center bg-gray-300"
  >
    <section class="w-full max-w-sm flex flex-col gap-4">
      <h2 class="text-sm text-gray-600 font-semibold uppercase tracking-widest">
        Element
      </h2>
      <div
        class="flex flex-col items-center justify-center p-6 gap-2 rounded shadow-md bg-white"
      >
        <div
          class="p-1 bg-green-200 text-green-900 rounded"
          :ref="elementApi.ref"
        >
          {{ elementMetadata }}
        </div>
      </div>
    </section>

    <section class="w-full max-w-sm flex flex-col gap-4">
      <h2 class="text-sm text-gray-600 font-semibold uppercase tracking-widest">
        List
      </h2>
      <div
        class="flex flex-col items-center justify-center p-6 gap-2 rounded shadow-md bg-white"
      >
        <div
          v-for="(item, index) in listMetadata"
          :ref="listApi.getRef(index)"
          :key="item"
          class="p-1 bg-green-200 text-green-900 rounded"
        >
          {{ item }}
        </div>
      </div>
    </section>

    <section class="w-full max-w-sm flex flex-col gap-4">
      <h2 class="text-sm text-gray-600 font-semibold uppercase tracking-widest">
        Plane
      </h2>
      <div
        class="flex flex-col items-center justify-center p-6 gap-2 rounded shadow-md bg-white"
      >
        <div
          v-for="(row, rowIndex) in planetMetadata"
          :key="row[0]"
          class="grid grid-cols-3 gap-2"
        >
          <div
            v-for="(column, columnIndex) in row"
            :ref="planeApi.getRef(rowIndex, columnIndex)"
            :key="column"
            class="p-1 line-clamp-1 bg-green-200 text-green-900 rounded"
          >
            {{ column }}
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script setup lang="ts">
import { elementMetadata } from "./elementMetadata";
import { listMetadata } from "./listMetadata";
import { planetMetadata } from "./planetMetadata";

import { onMounted } from "vue";

import { useElementApi } from "@baleada/vue-features";

const elementApi = useElementApi({ kind: "element" });
const listApi = useElementApi({ kind: "list" });
const planeApi = useElementApi({ kind: "plane" });

onMounted(() => {
  console.log("element", elementApi.element.value);
  console.log("list", listApi.elements.value);
  console.log("plane", planeApi.elements.value);
});
</script>
