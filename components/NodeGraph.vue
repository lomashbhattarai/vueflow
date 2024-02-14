<script setup>
import { VueFlow } from "@vue-flow/core";

import CustomNode from "../components/nodes/CustomNode.vue";

const elements = ref([
  // nodes

  {
    id: "1",
    type: "input",
    label: "Parent A",
    position: { x: 20, y: 200 },
    sourcePosition: "right",
    targetPosition: "right",
  },
  {
    id: "2",
    type: "input",
    label: "Parent B",
    position: { x: 20, y: 400 },
    sourcePosition: "right",
    targetPosition: "right",
  },

  // default node, you can omit `type: 'default'` as it's the fallback type
  { id: "3", label: "Node 2", position: { x: 300, y: 100 } },

  {
    id: "parent-1",
    label: "parent node",
    position: { x: 700, y: 100 },
    style: {
      backgroundColor: "rgba(16, 185, 129, 0.5)",
      width: "200px",
      height: "400px",
    },
    targetPosition: "left",
  },

  {
    id: "4",
    type: "output",
    label: "child node",
    position: { x: 10, y: 50 },
    parentNode: "parent-1",
    targetPosition: "left",
  },

  // A custom node, specified by using a custom type name
  // we choose `type: 'custom-node-1'` for this example
  {
    id: "5",
    type: "custom-node-1",
    label: "Node 4",
    position: { x: 300, y: 400 },
    targetPosition: "left",

    // pass custom data to the node
    data: {
      // you can pass any data you want to the node
      hello: "world",
    },
  },
  {
    id: "custom-node-data",
    type: "custom-node-2",
    label: "Custom Node 2",
    position: { x: 500, y: 300 },
    targetPosition: "left",

    // pass custom data to the node
    data: {
      // you can pass any data you want to the node
      hello: "world",
    },
  },

  // edges

  // an animated edge, specified by using `animated: true`
  { id: "e1-2", source: "1", target: "3", animated: true },

  {
    id: "e1-4",
    source: "1",
    target: "4",
  },
  { id: "e1-5", source: "1", target: "parent-1", animated: true },
  { id: "e2-5", source: "2", target: "5", animated: true },
  { id: "e2-6", source: "2", target: "custom-node-data", animated: false },
]);
</script>

<template>
  <VueFlow v-model="elements">
    <!-- bind your custom node type to a component by using slots, slot names are always `node-<type>` -->
    <template #node-custom-node-1="nodeProps">
      <CustomNode :message="nodeProps.data.hello" v-bind="nodeProps" />
    </template>
    <template #node-custom-node-2="nodeProps">
      <pre>{{ nodeProps }}</pre>
      <CustomNode :message="nodeProps.data.hello" v-bind="nodeProps" />
    </template>
  </VueFlow>
</template>

<style>
/* import the necessary styles for Vue Flow to work */
@import "@vue-flow/core/dist/style.css";

/* import the default theme, this is optional but generally recommended */
@import "@vue-flow/core/dist/theme-default.css";
</style>
