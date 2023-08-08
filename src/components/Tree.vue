<template>
  <el-tree-select
    size="large"
    v-model="value"
    :data="options"
    placeholder="Filter tree items"
    filterable
    :filter-node-method="handlerFilterNodeMethod">
    <template #default="{ data: { label, matched } }">
      <div v-html="matched?.str || label"></div>
    </template>
  </el-tree-select>
</template>

<script setup>
import { ElTreeSelect } from 'element-plus';
import { ref } from 'vue';
import { match } from 'sdm2';

const value = ref('');
const options = [
  {
    label: 'Fruit Tree',
    value: 10,
    children: [
      {
        label: 'Apple',
        value: 11,
        children: [
          {
            label: 'Red Apple',
            value: 12
          },
          {
            label: 'Green Apple',
            value: 13
          }
        ]
      },
      {
        label: 'Banana',
        value: 20,
        children: [
          {
            label: 'Regular Banana',
            value: 21
          },
          {
            label: 'Finger Banana',
            value: 22
          }
        ]
      }
    ]
  }
];

const handlerFilterNodeMethod = (query, node) => {
  const res = match(node.label, query, {
    ignoreCase: true,
    onMatched: (matchedStr) => `<span class="highlight">${matchedStr}</span>`
  });
  node.matched = res;
  return !!res;
}
</script>

<style>
.highlight {
  color: red;
}
</style>