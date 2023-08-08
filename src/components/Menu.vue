<template>
  <div>
    <el-input placeholder="Filter menu items" size="large" v-model="query"></el-input>
    <el-menu v-if="filteredMenus.length > 0" :default-openeds="[10, 11, 14, 20, 21].map(val => val + '')">
      <sub-menu
        v-for="menuItem in filteredMenus"
        :key="menuItem.value"
        :data="menuItem"></sub-menu>
    </el-menu>
    <el-empty description="menu not found" v-else />
  </div>
</template>

<script setup>
import { ElMenu, ElInput, ElEmpty } from 'element-plus';
import { computed, ref } from 'vue';
import { match } from 'sdm2';
import SubMenu from './SubMenu.vue';

const query = ref('');
const menus = [
	{
		label: 'Company Administration',
		value: 10,
		children: [
			{
				label: 'Employee Management',
				value: 11,
				children: [
					{
						label: 'Employee List',
						value: 12
					},
					{
						label: 'Employment and Termination Records',
						value: 13
					}
				]
			},
			{
				label: 'Department Management',
				value: 14,
				children: [
					{
						label: 'Department List',
						value: 15
					},
					{
						label: 'Department Organizational Structure',
						value: 16
					}
				]
			}
		]
	},
	{
		label: 'Sales Management',
		value: 20,
		children: [
			{
				label: 'Customer Management',
				value: 21,
				children: [
					{
						label: 'Customer List',
						value: 22
					},
					{
						label: 'Customer Analysis',
						value: 23
					}
				]
			},
			{
				label: 'Order Management',
				value: 24,
				children: [
					{
						label: 'Order List',
						value: 25
					},
					{
						label: 'Order Tracking',
						value: 26
					}
				]
			}
		]
	}
];


const filterTreeData = (tree, filterFn) => tree
  .map(treeItem => ({ ...treeItem }))
  .filter(treeItem => {
    let children = treeItem.children
    if (children && children.length > 0) {
      children = treeItem.children = filterTreeData(children, filterFn)
      if (children.length > 0) {
        filterFn(treeItem)
        return true
      }
    }
    return filterFn(treeItem)
  })
const filteredMenus = computed(() => filterTreeData(
  menus,
  menuItem => {
    const res = match(menuItem.label, query.value, {
      ignoreCase: true,
      onMatched: matchedStr => `<span class="highlight">${matchedStr}</span>`,
    })
    menuItem.matched = res;
    return !!res;
  }
));
</script>