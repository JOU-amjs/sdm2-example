<template>
  <el-select
    v-model="value"
    size="large"
    placeholder="Filter options"
    filterable
    :filter-method="q => (query = q)">
    <el-option
      v-for="item in optionsComputed"
      :key="item.value"
      :value="item.value"
      :label="item.label">
      <div v-html="item.highlight"></div>
    </el-option>
  </el-select>
</template>

<script setup>
import { ElSelect, ElOption } from 'element-plus';
import { computed, ref } from 'vue';
import { filterMap } from 'sdm2';

const value = ref('');
const options = [
  {
    value: 1,
    label: 'Elephant',
  },
  {
    value: 2,
    label: 'Adventure',
  },
  {
    value: 3,
    label: 'Sunshine',
  },
  {
    value: 4,
    label: 'Harmony',
  },
  {
    value: 5,
    label: 'Serendipity',
  },
  {
    value: 6,
    label: 'Midnight',
  },
  {
    value: 7,
    label: 'Blossom',
  },
  {
    value: 8,
    label: 'Wanderlust',
  },
];
const query = ref('');
const optionsComputed = computed(() => filterMap(options, query.value, {
  ignoreCase: true,
  matchStr: ({ label }) => label,
  onMatched: (matchedStr) => `<span class="highlight">${matchedStr}</span>`,
  onMap: ({ str, origin }) => {
    return {
      highlight: str,
      ...origin
    }
  }
}));
</script>