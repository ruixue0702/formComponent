<template>
	<div id="app">
		<div>
			<h3>Form组件</h3>
			<FormComponents/>
		</div>
	</div>
</template>

<script>
import FormComponents from '@/components/form'

export default {
	name: 'app',
	components: {
		FormComponents
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
</style>
