<template>
	<li class="treeLi">
		<div @click="toggle" class="treeLiCon">
			<span v-if="isFolder" class="iconOpen">{{open ? '-' : '+'}}</span>
			<span class="treeTitle">{{model.title}}</span>
		</div>
		<ul v-show="open" v-if="isFolder">
			<!-- 必须有结束条件 -->
			<item class="item" v-for="model in model.children" :model="model" :key="model.title"></item>
		</ul>
	</li>
</template>

<script>
export default {
	name: "Item", // name对递归组件是必要的
	props: {
		model: {
			type: Object,
			required: true
		}
	},
	data() {
		return {
			open: false
		};
	},
	computed: {
		isFolder() {
			return this.model.children && this.model.children.length;
		}
	},
	methods: {
		toggle() {
			if (this.isFolder) {
				this.open = !this.open;
			}
		}
	}
};
</script>
<style>
	ul {
		list-style: none;
		padding-left: 0;
	}
	.treeLi {
		padding-left: 30px;
		cursor: pointer;
	}
	.treeLiCon {
		padding: 3px;
		text-align: left;
	}
	.iconOpen {
		font-weight: bold;
		background: rgba(240, 138, 38, 0.8);
		color: #fff;
		line-height: 20px;
		width: 20px;
		display: inline-block;
		border-radius: 50%;
		margin-right: 5px;
		text-align: center;
	}
	.treeTitle {
		color: rgba(240, 138, 38, 1);
		display: inline-block;
		line-height: 26px;
	}
</style>
