<template>
  <el-menu-item 
    v-if="!data.children || data.children.length <= 0" 
    :index="data.value + ''">
    <el-icon>
      <location />
    </el-icon>
    <span v-html="data.matched?.str || data.label"></span>
  </el-menu-item>
  <el-sub-menu v-else :index="data.value + ''">
    <template #title>
      <el-icon>
        <icon-menu />
      </el-icon>
      <span v-html="data.matched?.str || data.label"></span>
    </template>
    <sub-menu
      v-for="childItem in data.children"
      :key="childItem.value"
      :data="childItem"></sub-menu>
  </el-sub-menu>
</template>

<script setup>
import { ElSubMenu, ElMenuItem, ElIcon } from 'element-plus';
import { Location, Menu as IconMenu } from '@element-plus/icons-vue';

defineProps({
  data: {
    type: Object,
    required: true
  }
});
</script>

<style scoped>

</style>