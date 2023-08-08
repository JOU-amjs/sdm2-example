<template>
  <div class="container">
    <Select></Select>
    <Tree></Tree>
    <Menu></Menu>
  </div>
</template>

<script setup>
import Menu from './components/Menu.vue';
import Select from './components/Select.vue'
import Tree from './components/Tree.vue'
</script>

<style>
.container {
  display: grid;
  grid-template-columns: repeat(2, 30%);
  grid-gap: 20px;
}
.highlight {
  color: red;
}
</style>
