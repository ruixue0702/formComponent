<template>
	<div id="app">
		<div>
			<h3 class="title">简单的Tree组件</h3>
			<div class="treeBox">
				<TreeComponents/>
			</div>
			
		</div>
	</div>
</template>

<script>
import TreeComponents from '@/components/tree'

export default {
	name: 'app',
	components: {
		TreeComponents
	}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.title {
	color: rgba(255, 138, 38, 1)
}
.treeBox {
	width: 300px;

}
</style>
