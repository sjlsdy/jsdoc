<template>
	<div id="app" class="layout-box">
		<div class="layout-left">
			<div class="nav">
				<ul>
					<li v-for="(item,index) in navData" :class="{ active: item.selected}" @click="setNav(index)">{{item.name}}</li>
				</ul>
			</div>
		</div>
		<div class="layout-left-secondary">
			<div class="nav">
				<ul v-if="navChildrenData.length > 0">
					<li v-for="(item,index) in navChildrenData" :class="{ active: item.selected}">{{item.name}}</li>
				</ul>
				<div v-else>
					请先选择分类
				</div>
			</div>
		</div>
		<div class="layout-main">
			<div class="layout-main-content">
				<router-view></router-view>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'app',
		data() {
			return {
				navData: [{
					name: 'ES6',
					src: 'es6',
					children: [{
						name: 'let const',
						src: 'let'
					}]
				}, {
					name: 'Date',
					src: 'date',
					children: [{
						name: 'constructor',
						src: 'constructor'
					}]
				}],
				navChildrenData: [],
			}
		},
		methods: {
			setNav(index) {
				for(let i = 0; i < this.navData.length; i++) {
					this.navData[i]['selected'] = false;
				}
				this.navData[index]['selected'] = true;
				this.navChildrenData = this.navData[index]['children'];
			}
		},

	}
</script>

<style>

</style>